---
name: Generate a dynamic QRIS with QRISLY
description: Upload a static QRIS once, then generate per-transaction dynamic QRIS codes with unique amounts and confirm payment by webhook or status poll.
api: openapi/komerce-qrisly-openapi.yml
operations:
  - uploadQris
  - generateQris
  - getQrisPaymentStatus
generated: '2026-07-19'
method: generated
---

# Generate a dynamic QRIS with QRISLY

QRISLY converts a merchant's **static** QRIS into **dynamic** per-transaction QRIS codes with
a fixed amount, so the buyer does not type the amount and you can reconcile automatically.

## Before you start

- Base URL: `https://api.collaborator.komerce.id/user` (sandbox:
  `https://api-sandbox.collaborator.komerce.id/user`).
- Auth: header `X-API-Key: <QRISLY_API_KEY>`, generated in the Collaborator dashboard under
  Developer -> API Settings -> Generate New API Key. Rotate roughly every 90 days.
- Cost: IDR 100 per generation, deducted from the balance wallet. API access, failed
  transactions, webhooks and QRIS management are free.

## Steps

1. **Upload the static QRIS — once.** Call `uploadQris` as `multipart/form-data` with
   `name` (max 100 chars) and `qris_image` (PNG or JPG, max 5MB). The image is validated
   automatically. Store the returned `data.qris_id` — you reuse it for every transaction.
2. **Generate per transaction.** Call `generateQris` with `qris_id`, `amount` (integer IDR,
   between 1000 and 100000000), `output_type` (`string` to render in-app, `image` to print),
   and `unique_amount`.
3. **Render.** The response gives `data.qris_string` (the EMVCo QR payload),
   `data.original_amount`, `data.final_amount`, `data.payment_status` and
   `data.expiry_time`. Default expiry is 15 minutes. Charge the buyer `final_amount`, not
   `original_amount`.
4. **Confirm payment.** Either poll `getQrisPaymentStatus` with the `history_id` from step 2,
   or register a webhook and handle `payment.success` / `payment.expired`.

## Why `unique_amount` matters

With `unique_amount: true`, QRISLY adds a small unique increment to the amount — IDR 10,000
becomes 10,001, then 10,002, then 10,003 for successive requests. The mobile listener app
reads the incoming payment amount from the merchant's banking app; without the increment two
identical payments are indistinguishable. Keep it `true` unless you have another way to
reconcile.

## Webhooks

Register at RajaOngkir dashboard -> Webhook -> QRISLY -> Outbound Webhook. QRISLY POSTs
`payment.success` and `payment.expired` events. Return
`200 OK` with `{"success": true, "message": "Webhook received and processed"}`. On failure
QRISLY retries 3 times with exponential backoff at 1, 5 and 15 minutes. Payloads are in
`asyncapi/komerce-webhooks.yml`.

## Errors

QRISLY uses a named error-code registry — `INVALID_API_KEY`, `RATE_LIMIT_EXCEEDED`,
`INVALID_QRIS_FORMAT`, `QRIS_NOT_FOUND`, `PAYMENT_EXPIRED`, `VALIDATION_ERROR`. Always check
the `success` field, not only the HTTP status. Full table in
`errors/komerce-error-codes.yml`.

Rate limits are signalled on `X-RateLimit-Limit`, `X-RateLimit-Remaining` and
`X-RateLimit-Reset`; on `429` read `Retry-After` and back off exponentially.

## Retry safety

`generateQris` is **not** idempotent and each call costs IDR 100. Never blind-retry it — on a
timeout, poll `getQrisPaymentStatus` for the `history_id` if you have one, or generate a
fresh code and let the previous one expire.
