# Komerce

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

Komerce is an Indonesian end-to-end e-commerce enabler serving more than 50,000 online sellers and SMEs with an integrated suite covering fulfilment, logistics, marketplace operations, CRM, advertising and payments — Komship, Kompack, Komplace, Komchat, Komcards, Komtim, Komads and Komclass. Its developer surface is published under the RajaOngkir brand and exposes four APIs: Shipping Cost (Cek Ongkir) for domestic and international rate lookup and airway-bill tracking across 17 Indonesian couriers, Shipping Delivery (Komship) for creating orders, requesting pickup, printing labels and tracking shipments, Payment Service for Virtual Account and QRIS transactions with signed callbacks, and QRISLY for turning a static QRIS into dynamic per-transaction QRIS codes. All four authenticate with a per-product header API key issued from the Collaborator dashboard, and the delivery, payment and QRIS products run a full isolated sandbox.

**Areas:** Company · Shipping · Logistics · E-Commerce · Payments · QRIS · Indonesia · Couriers · Tracking · Fulfillment

## Komerce on APIs.io

Everything profiled for Komerce is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/komerce/](https://apis.io/providers/komerce/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Komerce Cost API](https://apis.io/apis/komerce/komerce-cost-api/) — Shipping cost calculation
- [Komerce Destinations API](https://apis.io/apis/komerce/komerce-destinations-api/) — Destination and administrative-region lookup
- [Komerce Orders API](https://apis.io/apis/komerce/komerce-orders-api/) — The Orders API from Komerce — 4 operation(s) for orders.
- [Komerce Payments API](https://apis.io/apis/komerce/komerce-payments-api/) — The Payments API from Komerce — 4 operation(s) for payments.
- [Komerce Pickup API](https://apis.io/apis/komerce/komerce-pickup-api/) — The Pickup API from Komerce — 1 operation(s) for pickup.
- [Komerce QRIS API](https://apis.io/apis/komerce/komerce-qris-api/) — The QRIS API from Komerce — 3 operation(s) for qris.
- [Komerce Tracking API](https://apis.io/apis/komerce/komerce-tracking-api/) — Airway bill tracking

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Komerce Webhooks](https://apis.io/asyncapis/komerce/komerce-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [komerce](https://apis.io/servers/komerce/komerce/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Komerce Agentic Access](https://apis.io/agentic-access/komerce/komerce-agentic-access/)

#### Collections (14)

Postman and Open Collection request collections.

- [Komerce Payment Service Cost API](https://apis.io/collections/komerce/open-komerce-cost-api/)
- [Komerce Payment Service Cost Destinations API](https://apis.io/collections/komerce/open-komerce-destinations-api/)
- [Komerce Payment Service Cost Orders API](https://apis.io/collections/komerce/open-komerce-orders-api/)
- [Komerce Payment Service Cost Payments API](https://apis.io/collections/komerce/open-komerce-payments-api/)
- [Komerce Payment Service Cost Pickup API](https://apis.io/collections/komerce/open-komerce-pickup-api/)
- [Komerce Payment Service Cost QRIS API](https://apis.io/collections/komerce/open-komerce-qris-api/)
- [Komerce Payment Service Cost Tracking API](https://apis.io/collections/komerce/open-komerce-tracking-api/)
- [Komerce Payment Service Cost API](https://apis.io/collections/komerce/postman-komerce-cost-api/)
- [Komerce Payment Service Cost Destinations API](https://apis.io/collections/komerce/postman-komerce-destinations-api/)
- [Komerce Payment Service Cost Orders API](https://apis.io/collections/komerce/postman-komerce-orders-api/)
- [Komerce Payment Service Cost Payments API](https://apis.io/collections/komerce/postman-komerce-payments-api/)
- [Komerce Payment Service Cost Pickup API](https://apis.io/collections/komerce/postman-komerce-pickup-api/)
- [Komerce Payment Service Cost QRIS API](https://apis.io/collections/komerce/postman-komerce-qris-api/)
- [Komerce Payment Service Cost Tracking API](https://apis.io/collections/komerce/postman-komerce-tracking-api/)

#### Overlays (4)

OpenAPI overlays, including conversational phrasing for each operation.

- [Komerce Payment Overlay](https://apis.io/overlays/komerce/komerce-payment-overlay/)
- [Komerce Qrisly Overlay](https://apis.io/overlays/komerce/komerce-qrisly-overlay/)
- [Komerce Shipping Cost Overlay](https://apis.io/overlays/komerce/komerce-shipping-cost-overlay/)
- [Komerce Shipping Delivery Overlay](https://apis.io/overlays/komerce/komerce-shipping-delivery-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Komerce Authentication](https://apis.io/security/komerce/komerce-authentication/)
- [Komerce Domain Security](https://apis.io/security/komerce/komerce-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Komerce Plans](https://apis.io/plans/komerce/komerce-plans/)

#### Rate limits (1)

Published request limits.

- [Komerce Rate Limits](https://apis.io/rate-limits/komerce/komerce-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://komerce.id)
- [Documentation](https://rajaongkir.com/docs)
- [Getting started](https://rajaongkir.com/docs/introduction/register)
- [API reference](https://rajaongkir.com/docs/shipping-cost/getting_started/endpoint)
- [Pricing](https://rajaongkir.com/pricing)
- [Sign up](https://collaborator.komerce.id/registration)
- [Blog](https://komerce.id/blog/)
- [Terms of service](https://komerce.id/syarat-ketentuan)
- [Privacy policy](https://komerce.id/kebijakan-privasi)
- [Status](https://status.rajaongkir.com)

## API Evangelist rating

**Kin Score 45.9** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 23.7 |
| Contract governance | 19.7 |
| Operational transparency | 55.3 |
| Developer ergonomics | 70.8 |
| Access clarity | 48.7 |

**Agent readiness 36.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 15.2** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/komerce/](https://apis.io/providers/komerce/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Komerce: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/komerce/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
