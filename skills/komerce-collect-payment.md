---
name: Collect a payment with the Komerce Payment Service
description: List payment channels, create a Virtual Account or QRIS transaction, verify the HMAC-SHA256 signed callback, and reconcile the payment status.
api: openapi/komerce-payment-openapi.yml
operations:
  - getPaymentMethods
  - createPayment
  - getPaymentStatus
  - cancelPayment
generated: '2026-07-19'
method: generated
---

# Collect a payment with the Komerce Payment Service

## Before you start

- Base URL: `https://api.collaborator.komerce.id/user` (sandbox:
  `https://api-sandbox.collaborator.komerce.id/user`).
- Auth: headers `x-api-key: <API_KEY>` and `Content-Type: application/json`. This is the same
  key used for Komerce Shipping (RajaOngkir) — you do not need a separate one.
- Currency is IDR. Minimum amount is 10,000.
- Sandbox payments are simulated; no bank processes them.

## Steps

1. **List channels.** Call `getPaymentMethods`. Each entry gives `payment_type`
   (`va` or `qris`), `display_name`, `bank_code`, `logo_url`, `min_amount`, `max_amount`
   and `currency`. Render these as the buyer's payment options and use `bank_code` as the
   `channel_code` in the next step.
2. **Create the transaction.** Call `createPayment` with `order_id`, `payment_type`
   (e.g. `bank_transfer`), `channel_code`, `amount` (>= 10000), a `customer` object
   (`name`, `email`, `phone`), and `items[]` (`name`, `quantity`, `price`).
   Optionally set `expiry_duration` (minimum 3600 seconds), `callback_url`, and
   `callback_api_key` (required whenever `callback_url` is set — you generate this secret).
3. **Send the buyer to the hosted page.** The returned token addresses the prebuilt checkout
   at `https://pay.komerce.id/{token}` (sandbox `https://pay-sandbox.komerce.id/{token}`).
4. **Receive the callback.** Komerce POSTs to your `callback_url`. Verify it before trusting
   it — see below.
5. **Reconcile.** Call `getPaymentStatus` with the `payment_id` to confirm state, and treat
   the API as the source of truth over the callback.
6. **Cancel if abandoned.** `cancelPayment` cancels an unpaid Virtual Account payment.

## Verifying the callback (do not skip)

1. Take the **raw** JSON body exactly as received. Do not parse, reformat, or strip
   whitespace — any alteration changes the hash.
2. Read the signature from the `X-Callback-Api-Key` header. This header carries the
   signature, not your secret.
3. Compute `HMAC-SHA256(raw_body, callback_api_key)`.
4. Compare. On match, process and return `200 OK`. On mismatch, discard and return
   `401` or `403`.

## Fees and settlement

Virtual Account is a flat IDR 4,440 per transaction; QRIS is 0.99% per transaction. Both
include VAT and are deducted from settlement. Settlement is T+1. See
`plans/komerce-plans.yml`.

## Retry safety

There is **no idempotency key**. `order_id` is caller-supplied and is your only correlation
handle — before retrying a `createPayment` that timed out, look the transaction up rather
than blindly re-creating it, or you will strand two payment intents against one order.
