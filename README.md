# Komerce

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
