# Lab 01 — Excessive trust in client-side controls

> **Apprentice** · [Official lab](https://portswigger.net/web-security/logic-flaws/excessive-trust-in-client-side-controls)

**Entry point:** `POST /cart` — the `price` parameter is set by the client.

## Solution

1. Add the "Lightweight l33t leather jacket" to the cart and intercept
   `POST /cart`:

```
productId=1&redir=PRODUCT&quantity=1&price=133700
```

2. Change `price` to `1` and forward.
3. Checkout — the jacket costs $0.01 — lab solved.

## Mitigation

Recompute prices server-side from a trusted catalog; never trust
client-submitted totals or prices.
