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

Komerce is an Indonesian end-to-end e-commerce enabler serving more than 50,000 online sellers and SMEs with an integrated suite covering fulfilment, logistics, marketplace operations, CRM, advertising and payments — Komship, Kompack, Komplace, Komchat, Komcards, Komtim, Komads and Komclass.

Its developer surface is published under the **RajaOngkir** brand at [rajaongkir.com](https://rajaongkir.com) and exposes four APIs.

## APIs

| API | What it does | Base URL | Auth header |
|---|---|---|---|
| [Shipping Cost (Cek Ongkir)](https://rajaongkir.com/docs/shipping-cost/getting_started/about) | Destination lookup, domestic + international rate calculation across 17 Indonesian and 6 international couriers, AWB tracking | `https://rajaongkir.komerce.id/api/v1` | `key` |
| [Shipping Delivery (Komship)](https://rajaongkir.com/docs/delivery-order-api/getting_started/Getting-Started) | Create/cancel delivery orders, price regular/cargo/instant 3PL, pickup, labels, AWB history | `https://api.collaborator.komerce.id` | `x-api-key` |
| [Payment Service](https://rajaongkir.com/docs/payment-api/getting-started/getting-started) | Virtual Account + QRIS transactions, hosted payment page, HMAC-SHA256 signed callbacks | `https://api.collaborator.komerce.id/user` | `x-api-key` |
| [QRISLY](https://rajaongkir.com/docs/qrisly/getting-started/getting-started) | Static QRIS → dynamic per-transaction QRIS with unique amounts, payment webhooks | `https://api.collaborator.komerce.id/user` | `X-API-Key` |

The four keys are **not interchangeable** — each is issued separately from the Collaborator dashboard (Developer → Settings → Api Key). Sandbox and production also use separate keys.

## Artifacts in this repo

- `openapi/` — four OpenAPI 3.0.3 descriptions generated faithfully from the published RajaOngkir reference (Komerce publishes no machine-readable spec)
- `overlays/` — API Evangelist enhancement overlays for each spec
- `authentication/`, `conventions/`, `errors/`, `lifecycle/`, `sandbox/`, `conformance/`
- `asyncapi/komerce-webhooks.yml` — the three documented webhook surfaces (order status, payment callback, QRISLY events); no AsyncAPI is published
- `plans/`, `rate-limits/` — three-tier subscription (100 / 25,000 / 50,000 Cek Ongkir hits per day) plus per-transaction payment fees
- `vocabulary/komerce-couriers.yml` — courier code vocabulary and capability matrix
- `data-model/`, `examples/`, `packages/`, `components/`, `mcp/`, `skills/`, `llms/`
- `security/`, `well-known/`, `agentic-access/`

## Notable gaps

No published SDK on any registry (the WooCommerce plugin is the only first-party distributable), no OAuth, no idempotency key on any operation, no RFC 9457 errors, no security.txt or trust centre, and the System Update Log page is empty. The legacy rajaongkir.com API is flagged "will be deprecated" on the [status page](https://status.rajaongkir.com) but no deprecation policy is published.

Backed by: 500-global — https://komerce.id
