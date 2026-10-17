# Lab 03 — Multi-endpoint race conditions

> **Practitioner** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-multi-endpoint)

**Entry point:** checkout validates credit, but the order is confirmed
separately — race **two different endpoints** together.

## Solution

1. Put a gift card in the cart. Build a tab group:
   `POST /cart` (adds another gift card) + `POST /cart/checkout`.
2. Warm the connection with a leading `GET /` (removes first-request
   latency), then send the group in **parallel**.
3. The checkout validated the small cart, but the parallel cart-add lands
   inside the window — the confirmation includes **extra gift cards** you
   didn't pay for.
4. Redeem them until your credit covers the jacket, buy it — lab solved.

## Mitigation

Enforce state transitions atomically (row locks / transactions spanning
add-to-cart, validate, confirm).
