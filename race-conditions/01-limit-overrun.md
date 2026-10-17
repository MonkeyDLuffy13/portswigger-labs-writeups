# Lab 01 — Limit overrun race conditions

> **Practitioner** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-limit-overrun)

**Entry point:** `POST /cart/coupon` — the "Coupon already applied" check
has a race window before the DB is updated.

## Solution

1. Add any item; capture `POST /cart/coupon` (your CSRF + code).
2. Fire ~20 copies **in parallel** (Repeater tab group → *Send group in
   parallel (single-packet attack)* — or the built-in *Trigger race
   condition* custom action template).
3. Refresh the cart: the 20% discount applied **multiple times** — order is
   far cheaper — checkout — lab solved.

## Notes

The single-packet attack aligns all requests within one TCP packet so they
hit the handler simultaneously.
