---
generated: '2026-09-19'
method: generated
name: xguardgate-com-secretless-egress
description: As an operator, store an upstream credential and issue a scoped capability; as an agent, make an idempotent credential-backed upstream call through XGuard and handle 409/402/503 the way the contract requires; then revoke.
api: openapi/xguardgate-com-openapi.json
operations: []
routes: ['POST /v1/egress/credentials', 'POST /v1/egress/capabilities', 'POST /v1/egress/fetch', 'DELETE /v1/egress/capabilities/{id}', 'GET /v1/egress/providers']
source: >-
  Grounded in openapi/xguardgate-com-openapi.json (none of these routes declares an operationId; method + path
  are as published), https://api.xguardgate.com/.well-known/xguard-egress.json, docs/secretless-outcomes.md and
  sdk/README.md. Live probes 2026-09-19: GET /v1/egress/providers 200; GET /v1/egress/credentials 401
  xguard_key_required without a key. No credential was stored and no upstream call was made.
---

# Delegate an upstream API call without giving the agent the secret

Two roles. The OPERATOR holds an X-XGuard-Key and prepaid Usage Credits, stores the vendor secret once, and mints short-lived scoped capabilities. The AGENT receives only a capability (`xgc_...`) and calls the vendor through XGuard, which injects the credential at egress and returns a signed proof. Supported providers: openai, anthropic, github, stripe, slack, notion, cloudflare, gemini, or `custom {header_name, allowed_hosts}`.

## Auth
- Operator routes: header `X-XGuard-Key` (401 `xguard_key_required` without it). Agent route: the capability string in the request body (401 `capability_required`). Never put the operator key in an agent prompt. See `authentication/xguardgate-com-authentication.yml`.

## Operator steps
1. **See what is supported** - `GET /v1/egress/providers` (public): hosts and injection header per provider (e.g. anthropic -> api.anthropic.com, `x-api-key`).
2. **Store the credential** - `POST /v1/egress/credentials` with `X-XGuard-Key`. Restrict origin, paths and methods. 201 returns metadata and a `credential_id`; the secret is never returned. Requires Usage Credits (JOD 3.550 per 5,000, card checkout).
3. **Issue a capability** - `POST /v1/egress/capabilities` with `{"credential_id": ..., "target_origin": "https://api.github.com", "path_prefix": "/repos/your-org/your-repo/", "allowed_methods": ["POST"], "ttl_seconds": 900, "max_calls": 5, "max_total_credits": 5, "max_credits_per_call": 1}`. `ttl_seconds` is 30-3600. 201 returns the scoped capability; keep the returned capability id for revocation and pass ONLY the capability to the agent.

## Agent steps
4. **Call through XGuard, idempotently** - `POST /v1/egress/fetch` with `{"capability": "<xgc_...>", "target": "https://api.github.com/repos/your-org/your-repo/issues", "method": "POST", "idempotency_key": "support-case-123-v1", "body_json": {"title": "Investigate customer case 123"}}` (header `Idempotency-Key` is accepted too and must equal the body key). The key is REQUIRED for POST/PUT/PATCH/DELETE (400 before billing without it); 8-128 chars of `[A-Za-z0-9_:.-]`; make it a stable business key. Add `idempotency_key` to a GET only if you want replay protection.
5. **Read the result** - the upstream status and body come back with `x-xguard-execution-id`, `x-xguard-proof` (ES256, verify at `POST /v1/proofs/verify`) and, on a replay, `X-XGuard-Replay: true`. Results are capped at 48 KiB; redirects are returned, not followed. Validate the upstream HTTP status before treating the action as done.
6. **Retry with the SAME key** - identical request -> stored response, no new charge, no second upstream call.

## Operator step
7. **Revoke** - `DELETE /v1/egress/capabilities/{id}` with `X-XGuard-Key`. New attempts and stored-result access are denied; "already dispatched work may finish". 403 if you are not the owner.

## Errors (the ones that matter)
- `409 idempotency_request_conflict` - same key, different request. Fix the request or use a NEW business operation; do not reuse the key.
- `409 execution_in_progress` - a concurrent copy is running; poll with the same key.
- `409 execution_outcome_unknown` - XGuard reserved credits but cannot prove the upstream outcome. It will never re-execute automatically. Do NOT rotate the key to force a retry; escalate to a human or check the vendor.
- `402` - price exceeds `max_credits_per_call` / remaining budget (before billing). `403` - scope denied. `503` - billing/decryption/network ambiguity; no automatic replay.

## Notes
- Guarantee is "at most one XGuard upstream attempt per capability and key", not distributed exactly-once. Vendor fees are billed to the operator by the vendor. Replay is available only while the capability is valid; encrypted results are deleted 24 h after expiry - store receipts you need in your own audit system.
- Full contract: `conventions/xguardgate-com-conventions.yml` (idempotency, reversibility) and `errors/xguardgate-com-problem-types.yml`.
