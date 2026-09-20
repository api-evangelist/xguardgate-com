---
generated: '2026-09-19'
method: generated
name: xguardgate-com-free-extraction-preview
description: Get a real, free XGuard extraction result from labelled sample data or your own HTML, with no account, key or wallet, and read the response envelope correctly.
api: openapi/xguardgate-com-openapi.json
operations: [xguardExecute]
routes: ['POST /v1/execute', 'GET /v1/capabilities']
source: >-
  Grounded in openapi/xguardgate-com-openapi.json (xguardExecute), https://xguardgate.com/try, the README and
  a live probe on 2026-09-19 (POST /v1/execute {"intent":"demo"} -> 200, cost 0.000000 USDC).
---

# Free extraction preview

Use XGuard's parser on labelled sample HTML or on HTML you already have. No outbound request is made, nothing is charged, and no credential is needed. This is the provider's intended first call and the rehearsal for the paid outcomes.

## Auth
- None. Do not send X-XGuard-Key, Payment-Signature or a wallet. See `authentication/xguardgate-com-authentication.yml`.

## Steps
1. (Optional) **Discover** - `GET /v1/capabilities` (no operationId in the spec). Read `capabilities[]` for the four ids, their `input_schema`, prices and examples. `extract-preview` has `amount "0.000000"`.
2. **Execute the demo** - `xguardExecute` (`POST /v1/execute`, `content-type: application/json`) with body `{"intent":"demo"}`. Expect HTTP 200 and `result.data_mode: "labelled_sample"`, `result.network_calls: 0`, `cost.amount: "0.000000"`, `receipt: null`, `verification.signed: false`.
3. **Or parse your own HTML** - the same operation with `{"intent":"Extract this page","html":"<html>...</html>"}`; `html` is capped at 12,288 characters (`413` above that). Do not paste credentials or private documents - the provider says so on /try.
4. **Read the envelope** - `ok`, `request_id` (also in `x-xguard-request-id`), `intent.capability`, `result.document{title, description, text, links}`, `result.offers[]` (Schema.org offers with `verification` notes), `result.input_sha256`, `verification.result_sha256`, and `next` (the suggested paid example).

## Errors
- `422 capability_unavailable` with `repair.suggested_request` and `closest_capabilities[]` when the intent matches nothing (e.g. an empty body) - resend `repair.suggested_request`.
- `413` when `html` exceeds the cap. All failures use the `ok:false / error.code / next` envelope in `errors/xguardgate-com-problem-types.yml`.

## Notes
- `result.notice` says "Sample product and price; no merchant was contacted." The sample offer (gtin 00123456789012, 12.50 USD) is demonstration data - never present it as a live price.
- The same call is available as MCP tool `xguard_execute` and A2A skill `extract-preview`.
