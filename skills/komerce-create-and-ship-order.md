---
name: Create a Komship delivery order and ship it
description: Resolve destinations, price the delivery, create the order, request pickup, print the label, and track the airway bill through the Komerce Shipping Delivery API.
api: openapi/komerce-shipping-delivery-openapi.yml
operations:
  - searchDeliveryDestination
  - calculateDeliveryPrice
  - storeOrder
  - requestPickup
  - printOrderLabel
  - getOrderDetail
  - getAirwayBillHistory
  - cancelOrder
generated: '2026-07-19'
method: generated
---

# Create a Komship delivery order and ship it

## Before you start

- Base URL: `https://api.collaborator.komerce.id` (sandbox:
  `https://api-sandbox.collaborator.komerce.id`). Always build against sandbox first.
- Auth: header `x-api-key: <SHIPPING_DELIVERY_API_KEY>`. Sandbox and production use
  **separate keys**, and a Shipping Cost or QRISLY key will not work here.
- Weight for this API is in **kilograms**, decimal, dot separator.
- Bank-transfer orders draw down the Collaborator dashboard balance at creation time.

## Steps

1. **Resolve both addresses.** Call `searchDeliveryDestination` with `keyword` set to a
   subdistrict name or zip code. Take `data[].id` for the shipper and again for the receiver;
   these become `shipper_destination_id` and `receiver_destination_id`.
2. **Price the delivery.** Call `calculateDeliveryPrice` with
   `shipper_destination_id`, `receiver_destination_id`, `origin_pin_point`,
   `destination_pin_point` (both `"lat,lng"`), `weight` in kg, `item_value`, and
   `cod=yes` if you need COD coverage for the route. The response splits into
   `data.calculate_reguler`, `data.calculate_cargo` and `data.calculate_instant`. Pick a
   courier and service and carry its cost forward.
3. **Create the order.** Call `storeOrder` with the JSON body. Required: `order_date`,
   `brand_name`, shipper and receiver name/phone/destination_id/address, `shipper_email`,
   `shipping` (courier), `shipping_type` (service), `payment_method`
   (`COD` or `BANK TRANSFER`), `shipping_cost`, and `order_details[]` with product name,
   price, weight, dimensions, qty and subtotal.
4. **Request pickup.** Call `requestPickup` with the `order_no` and the desired pickup
   date/time.
5. **Print the label.** Call `printOrderLabel` with `order_no` and a `page` layout such as
   `page_5`.
6. **Track.** Poll `getAirwayBillHistory` with `shipping` (courier code) and `airway_bill`,
   or read `getOrderDetail` by `order_no`. Better: register a webhook and let Komerce push
   status changes to you (see below).
7. **Cancel if needed.** `cancelOrder` (PUT) with the `order_no`.

## Hard validation rules

- Phone numbers **must** start with `0` or `62` — `081234567890` or `6281234567890`.
  A leading `+62` is rejected.
- If `payment_method` is `BANK TRANSFER` and the dashboard balance is less than the shipping
  charge, the order is **not** created and an error is returned. Check balance before
  batch-creating orders.
- Incorrect destination ids silently produce wrong shipping costs — always resolve ids via
  step 1 rather than caching stale ids.

## Events instead of polling

Register a webhook handler URL (PUT to `/webhook` with your URL) and Komerce pushes
`{ order_no, cnote, status }` on every status change — `Diajukan`, `Dijemput`, `Dikirim`,
`Dibatalkan`, `Selesai`. Return HTTP 200 or Komerce may retry and eventually deactivate the
webhook. Details in `asyncapi/komerce-webhooks.yml`.

## Retry safety

There is **no idempotency key** on `storeOrder`. A retried create can produce a duplicate
order and a duplicate balance deduction. Before retrying a create that timed out, call
`getOrderDetail` with your `order_no` to check whether the first attempt landed.
