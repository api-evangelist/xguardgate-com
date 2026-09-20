---
generated: '2026-09-19'
method: generated
name: xguardgate-com-paid-outcome-x402
description: Run a paid public-source outcome (web-extraction, product-offers or feed-digest) through the x402 v2 quote -> 402 -> sign -> retry flow, within an explicit budget, and recover the result without ever paying twice.
api: openapi/xguardgate-com-openapi.json
operations: [xguardExecute]
routes: ['POST /v1/pricing/quote', 'POST /v1/execute', 'GET /v1/results/{payment_identifier}', 'GET /v1/operations/{payment_identifier}']
source: >-
  Grounded in openapi/xguardgate-com-openapi.json, https://xguardgate.com/developers, sdk/README.md and
  docs/public-gateway-contract.md, plus live probes on 2026-09-19 (POST /v1/pricing/quote -> 200 signed quote;
  POST /v1/execute with a paid intent -> 402 with Payment-Required and X-XGuard-Quote; nothing was paid).
---

# Run a paid outcome with x402

XGuard sells three live outcomes per execution in USDC on Base (eip155:8453): `web-extraction` 0.003, `product-offers` 0.006, `feed-digest` 0.002. Payment is the authorization; there is no account. You need a caller-owned wallet funded with Base USDC and an x402 v2 client (the provider points at `@x402/core` / `@x402/evm` and, for MCP, `@x402/mcp`).

## Auth
- None for discovery and quoting. Payment headers on the retry: `Payment-Signature` (x402 v2 signed authorization) and the preserved `X-XGuard-Quote`. See `authentication/xguardgate-com-authentication.yml`.

## Budget first
- Decide the maximum atomic USDC you will spend (`2000` = 0.002 USDC). The official SDK refuses to sign outside `maxAmountAtomic` and defaults it to zero; do the same.

## Steps
1. (Optional) **Quote** - `POST /v1/pricing/quote` with `{"capability":"feed-digest"}` (or `tool_id`). Free. Response carries `quote` (a 300-second ES256 JWS), `next.body` and `next.execution_url`. You may skip this: an unsigned call in step 2 produces the same quote.
2. **Request without payment** - `xguardExecute` (`POST /v1/execute`) with the exact intent, e.g. `{"intent":"Get a technology news digest","limit":10}` or `{"intent":"Extract these pages","urls":["https://example.com/","https://www.iana.org/help/example-domains"]}` (urls <= 3). Expect HTTP 402: header `Payment-Required` (base64url x402 v2 object), header `X-XGuard-Quote`, header `x-xguard-payment-identifier`, body `{status:"payment_required", price{amount_atomic, amount, currency}, expires_at, retry{preserve_body:true, preserve_headers:["X-XGuard-Quote"], payment_header:"Payment-Signature"}, accepts[{scheme:"exact", network:"eip155:8453", asset, payTo, amount, maxTimeoutSeconds:300}]}`. `target_contacted` is false - nothing has been fetched.
3. **Check the challenge against your budget** - `accepts[0].amount` must be <= your cap, `network` must be `eip155:8453` (or `eip155:84532` if you set `"testnet": true`), `asset` must be USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`. Abort otherwise.
4. **Sign and retry** - have the x402 client sign `Payment-Required`, then resend the IDENTICAL body to the same URL with `Payment-Signature` and the unchanged `X-XGuard-Quote`. Save the payment identifier + quote durably BEFORE sending (the SDK's `onPaymentPrepared`). XGuard verifies and settles, then fetches. Expect 200 with `result`, `cost`, `receipt`, `Payment-Response`, `x-xguard-receipt` and `x-xguard-proof`.
5. **Recover, never re-pay** - on a timeout or lost response, `GET /v1/results/{payment_identifier}` with header `X-XGuard-Quote: <original quote>`. 200 returns the stored outcome; 202 means pending or credited (no re-execution); 403 means the quote does not match; 404 unknown. `GET /v1/operations/{payment_identifier}` shows the financial state. Treat the quote as a private bearer token.

## Errors
- `502 No usable source; execution credit retained` - every source and fallback failed after settlement. Retry the same outcome with header `X-XGuard-Credit` plus the original quote; do not pay again. This is not a cash refund.
- `503` settlement awaiting reconciliation - do not start a new purchase; poll step 5 or, for Base timeouts, the Reconcile API at reconcile.xguardgate.com.
- `409` replay/idempotency conflict, `413` too large, `429` rate limit (no headers), `403` unsafe target. Envelope in `errors/xguardgate-com-problem-types.yml`.

## Notes
- Prices include bounded fallback; quantity is exactly one execution; the quote expires in 300 s - re-request rather than reuse an expired one.
- A source digest proves what was observed, not that it is true or that a merchant price is current at checkout.
- MCP twin: `xguard_execute` returns an `isError` result carrying the same challenge; retry identical arguments with `params._meta["x402/payment"]`; recover with `xguard_get_result`.
