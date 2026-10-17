# Lab 02 — High-level logic vulnerability

> **Practitioner** · [Official lab](https://portswigger.net/web-security/logic-flaws/high-level-logic-vulnerability)

**Entry point:** `POST /cart` — `quantity` accepts negative values.

## Solution

1. Add a cheap item, intercept `POST /cart`, and confirm the quantity is
   client-controlled — including **negative** numbers.
2. Strategy: order a large positive quantity of the cheap item (its discount
   coupon builds credit), then use negative quantities to keep only the
   leather jacket while driving the total under your store credit:

   - add the jacket (positive),
   - add a large negative quantity of the cheap item until the total drops
     below your remaining credit (the cart may hold negative units of the
     cheap item while showing the jacket).

3. Checkout with the total inside your credit — lab solved.

## Notes

State machines must validate every transition: quantities ≤ 0, totals ≥ 0,
and item presence should all be enforced server-side.
