# Lab 10 — Infinite money logic flaw

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/infinite-money)

**Entry point:** buy $10 gift card with a 30% coupon ($7), redeem for $10
credit → +$3 per cycle. Automate with a Burp macro.

## Solution

1. Sign up for the newsletter → `SIGNUP30` coupon. Buy a $10 gift card,
   apply the coupon at checkout, redeem it — store credit +$3.
2. Automate: Settings → Sessions → add rule (scope: all URLs) running a
   macro of the 5-request cycle:

```
POST /cart
POST /cart/coupon        (apply SIGNUP30)
POST /cart/checkout
GET  /cart/order-confirmation?order-confirmed=true
POST /gift-card          (redeem the new code)
```

Configure the macro to extract the new `gift-card` code from the order
confirmation response (response 4) and inject it into the redeem request.
3. Send `GET /my-account` in Intruder with null payloads / continue
   indefinitely until credit ≥ $1337 (jacket price).
4. Buy the jacket — lab solved.

## Notes

Any arbitrage loop (discount > value, refundable item) is an infinite
money printer — cap negative margins.
