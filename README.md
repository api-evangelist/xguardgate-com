# XGuard

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

XGuard is a paid-tool and credential-brokering gateway for AI agents, operated from xguardgate.com with its API at api.xguardgate.com and its source published at github.com/moelayyan90/XGuard (Apache-2.0, Cloudflare Workers). Its canonical product, "XGuard Universal Paid AI Agent + Secretless Gateway" (v5.1.0), sells four public-source outcomes to any agent with no account or API key: a free HTML extraction preview, multi-page evidence extraction, Schema.org product-offer comparison and a deduplicated RSS/Atom feed digest, each priced per execution in USDC on Base (0.002-0.006 USDC) and settled through the x402 v2 protocol before the sources are touched, with a signed quote, a replay-safe payment identifier, a signed receipt and ES256 "ProofRail" execution evidence. A second surface, Secretless Egress, lets an operator store an upstream API credential (OpenAI, Anthropic, GitHub, Stripe, Slack, Notion, Cloudflare, Gemini or custom) and hand an agent a short-lived scoped capability instead of the secret, with a mandatory Idempotency-Key on every write. The same catalog is exposed as a 49-operation OpenAPI 3.1.0 contract, a remote Streamable HTTP MCP server at api.xguardgate.com/mcp that answers tools/list anonymously, an A2A 1.0.0 agent card at /.well-known/agent-card.json, an OpenAI plugin manifest, llms.txt and a set of x402 payment, egress and action manifests; a companion x402 settlement-reconciliation API runs at reconcile.xguardgate.com.

**Areas:** Agents · Agentic Commerce · x402 · MCP · A2A · Micropayments · Web Extraction · Feed Aggregation · Credential Broker · API Gateway · Agent Security · Agent-Native

## XGuard on APIs.io

Everything profiled for XGuard is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/xguardgate-com/](https://apis.io/providers/xguardgate-com/)** — or go straight to one of the APIs or properties below.

### APIs (30)

- [XGuard MCP Server](https://apis.io/apis/xguardgate-com/xguard-mcp-server/) — Remote Model Context Protocol server at https://api.xguardgate.com/mcp (Streamable HTTP, protocol version 2026-07-28, serverInfo…
- [XGuard A2A Agent](https://apis.io/apis/xguardgate-com/xguard-a2a-agent/) — Agent2Agent surface: an agent card served identically from https://api.xguardgate.com/.well-known/agent-card.json (the canonical location named in the…
- [XGuard Actions API](https://apis.io/apis/xguardgate-com/xguardgate-com-actions-api/) — The Actions API from XGuard — 5 operation(s) for actions.
- [XGuard Agent Card.json API](https://apis.io/apis/xguardgate-com/xguardgate-com-agent-card-json-api/) — The Agent Card.json API from XGuard — 1 operation(s) for agent card.json.
- [XGuard Discovery API](https://apis.io/apis/xguardgate-com/xguardgate-com-discovery-api/) — The Discovery API from XGuard — 2 operation(s) for discovery.
- [XGuard Edge API](https://apis.io/apis/xguardgate-com/xguardgate-com-edge-api/) — The Edge API from XGuard — 1 operation(s) for edge.
- [XGuard Egress API](https://apis.io/apis/xguardgate-com/xguardgate-com-egress-api/) — The Egress API from XGuard — 6 operation(s) for egress.
- [XGuard Facilitator API](https://apis.io/apis/xguardgate-com/xguardgate-com-facilitator-api/) — The Facilitator API from XGuard — 2 operation(s) for facilitator.
- [XGuard Health API](https://apis.io/apis/xguardgate-com/xguardgate-com-health-api/) — The Health API from XGuard — 1 operation(s) for health.
- [XGuard Healthz API](https://apis.io/apis/xguardgate-com/xguardgate-com-healthz-api/) — The Healthz API from XGuard — 1 operation(s) for healthz.
- [XGuard Inspect API](https://apis.io/apis/xguardgate-com/xguardgate-com-inspect-api/) — The Inspect API from XGuard — 1 operation(s) for inspect.
- [XGuard Metrics API](https://apis.io/apis/xguardgate-com/xguardgate-com-metrics-api/) — The Metrics API from XGuard — 1 operation(s) for metrics.
- [XGuard Openapi.yaml API](https://apis.io/apis/xguardgate-com/xguardgate-com-openapi-yaml-api/) — The Openapi.yaml API from XGuard — 1 operation(s) for openapi.yaml.
- [XGuard Operations API](https://apis.io/apis/xguardgate-com/xguardgate-com-operations-api/) — The Operations API from XGuard — 1 operation(s) for operations.
- [XGuard Outcomes API](https://apis.io/apis/xguardgate-com/xguardgate-com-outcomes-api/) — Primary intent execution
- [XGuard Payment API](https://apis.io/apis/xguardgate-com/xguardgate-com-payment-api/) — The Payment API from XGuard — 1 operation(s) for payment.
- [XGuard Preflight API](https://apis.io/apis/xguardgate-com/xguardgate-com-preflight-api/) — The Preflight API from XGuard — 1 operation(s) for preflight.
- [XGuard Pricing API](https://apis.io/apis/xguardgate-com/xguardgate-com-pricing-api/) — The Pricing API from XGuard — 2 operation(s) for pricing.
- [XGuard Proof API](https://apis.io/apis/xguardgate-com/xguardgate-com-proof-api/) — The Proof API from XGuard — 1 operation(s) for proof.
- [XGuard Proofs API](https://apis.io/apis/xguardgate-com/xguardgate-com-proofs-api/) — The Proofs API from XGuard — 1 operation(s) for proofs.
- [XGuard Protocols API](https://apis.io/apis/xguardgate-com/xguardgate-com-protocols-api/) — The Protocols API from XGuard — 1 operation(s) for protocols.
- [XGuard Ready API](https://apis.io/apis/xguardgate-com/xguardgate-com-ready-api/) — The Ready API from XGuard — 1 operation(s) for ready.
- [XGuard Receipts API](https://apis.io/apis/xguardgate-com/xguardgate-com-receipts-api/) — The Receipts API from XGuard — 1 operation(s) for receipts.
- [XGuard Reconcile API](https://apis.io/apis/xguardgate-com/xguardgate-com-reconcile-api/) — The Reconcile API from XGuard — 1 operation(s) for reconcile.
- [XGuard Settle API](https://apis.io/apis/xguardgate-com/xguardgate-com-settle-api/) — The Settle API from XGuard — 1 operation(s) for settle.
- [XGuard Supported API](https://apis.io/apis/xguardgate-com/xguardgate-com-supported-api/) — The Supported API from XGuard — 1 operation(s) for supported.
- [XGuard Test API](https://apis.io/apis/xguardgate-com/xguardgate-com-test-api/) — The Test API from XGuard — 2 operation(s) for test.
- [XGuard Tools API](https://apis.io/apis/xguardgate-com/xguardgate-com-tools-api/) — The Tools API from XGuard — 2 operation(s) for tools.
- [XGuard Verify API](https://apis.io/apis/xguardgate-com/xguardgate-com-verify-api/) — The Verify API from XGuard — 1 operation(s) for verify.
- [XGuard .well Known API](https://apis.io/apis/xguardgate-com/xguardgate-com-well-known-api/) — The .well Known API from XGuard — 3 operation(s) for .well known.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [XGuard Universal Paid AI Agent + Secretless Gateway](https://apis.io/servers/xguardgate-com/xguard-universal-paid-secretless-gateway/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Xguardgate Com Agentic Access](https://apis.io/agentic-access/xguardgate-com/xguardgate-com-agentic-access/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Xguardgate Com Openapi Overlay](https://apis.io/overlays/xguardgate-com/xguardgate-com-openapi-overlay/)
- [Xguardgate Com Reconcile Openapi Overlay](https://apis.io/overlays/xguardgate-com/xguardgate-com-reconcile-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Xguardgate Com Authentication](https://apis.io/security/xguardgate-com/xguardgate-com-authentication/)
- [Xguardgate Com Domain Security](https://apis.io/security/xguardgate-com/xguardgate-com-domain-security/)
- [Xguardgate Com Vulnerability Disclosure](https://apis.io/security/xguardgate-com/xguardgate-com-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Xguardgate Com Plans Pricing](https://apis.io/plans/xguardgate-com/xguardgate-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Xguardgate Com Rate Limits](https://apis.io/rate-limits/xguardgate-com/xguardgate-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://xguardgate.com/)
- [Documentation](https://xguardgate.com/developers)
- [Getting started](https://xguardgate.com/connect)
- [API reference](https://api.xguardgate.com/openapi.json)
- [Pricing](https://xguardgate.com/pricing)
- [Support](https://github.com/moelayyan90/XGuard/issues)
- [Terms of service](https://xguardgate.com/terms)
- [Privacy policy](https://xguardgate.com/privacy)

## API Evangelist rating

**Kin Score 52.4** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 40.1 |
| Contract governance | 18.2 |
| Operational transparency | 31.6 |
| Developer ergonomics | 57.7 |
| Access clarity | 63.2 |

**Agent readiness 46.5** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | verified |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | documented (partial credit) |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | mostly (partial credit) |

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/xguardgate-com/](https://apis.io/providers/xguardgate-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for XGuard: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/xguardgate-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
