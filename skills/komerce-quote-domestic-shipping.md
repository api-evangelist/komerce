---
name: Quote domestic shipping with RajaOngkir
description: Resolve an Indonesian origin and destination to RajaOngkir destination ids, then quote shipping cost across couriers for a given package weight.
api: openapi/komerce-shipping-cost-openapi.yml
operations:
  - searchDomesticDestination
  - calculateDomesticCost
generated: '2026-07-19'
method: generated
---

# Quote domestic shipping with RajaOngkir

Use this skill to turn a human address into a shipping quote across Indonesian couriers.

## Before you start

- Base URL: `https://rajaongkir.komerce.id/api/v1`
- Auth: send the header `key: <SHIPPING_COST_API_KEY>` on every request. This is the
  **Shipping Cost** key from the Collaborator dashboard (Developer -> Settings -> Api Key).
  A Shipping Delivery or QRISLY key will fail with 401.
- Weight for this API is in **grams** (integer).

## Steps

1. **Resolve the origin.** Call `searchDomesticDestination` with `search` set to the origin
   city, district, subdistrict, or postal code. Optionally page with `limit` and `offset`.
   Read `data[].id` from the match whose `label` matches the intended address — the label is
   formatted `SUBDISTRICT, DISTRICT, CITY, ZIP`.
2. **Resolve the destination.** Call `searchDomesticDestination` again for the recipient
   address and take its `data[].id`.
3. **Quote.** Call `calculateDomesticCost` with an
   `application/x-www-form-urlencoded` body: `origin` (step 1 id), `destination` (step 2 id),
   `weight` in grams, and `courier` as a courier code. Add `price=lowest` or `price=highest`
   to bias selection.
4. **Read the quote.** Each `data[]` entry carries `name`, `code`, `service`, `description`,
   `cost` and `etd`. Present these as the shipping options.

## Courier codes

Valid `courier` values are in `vocabulary/komerce-couriers.yml`: `jne`, `sicepat`, `ide`,
`sap`, `ninja`, `jnt`, `tiki`, `wahana`, `pos`, `sentral`, `lion`, `rex`. Not every courier
supports every capability — check the matrix before quoting.

## Rules

- Cache province and courier reference data locally; it changes rarely and every call spends
  daily quota (100/day on Starter, 25,000 on Pro, 50,000 on Enterprise).
- Debounce destination search when driving an autocomplete field.
- There is **no idempotency key** — a retried `calculateDomesticCost` is simply another
  quota-consuming read. It is safe to retry because it has no side effects.
- On `401`, check the key is the Shipping Cost key, is active, has no stray whitespace, and
  that the request is HTTPS.
- On `429`, read `Retry-After` and back off exponentially.
- Errors return `{ meta: { message, code, status } }` — check `meta.code`, not just the HTTP
  status. See `errors/komerce-problem-types.yml`.

## Alternative: cascading selection

If your UI collects address by dropdown rather than search, use `listProvinces`,
`listCities`, `listDistricts` and `listSubdistricts` to cascade, then quote with
`calculateDistrictDomesticCost` instead of `calculateDomesticCost`.
