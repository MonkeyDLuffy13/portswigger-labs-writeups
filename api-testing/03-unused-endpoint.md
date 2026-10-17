# Lab 03 — Finding and exploiting an unused API endpoint

> **Practitioner** · [Official lab](https://portswigger.net/web-security/api-testing/lab-exploiting-unused-api-endpoint)

**Entry point:** `GET /api/products/1/price` — an unused PATCH handler.

## Solution

1. `OPTIONS /api/products/1/price` → allowed: `GET, PATCH`.
2. Log in, PATCH with `Content-Type: application/json`, body `{"price":0}`.
3. Reload the jacket page — price is now $0.00 — add to basket, place
   order — lab solved.

## Notes

Unused/unlinked API methods are common; enumerate methods with OPTIONS and
method-guessing.
