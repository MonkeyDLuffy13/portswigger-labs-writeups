# Lab 11 — User ID controlled by request parameter with data leakage in redirect

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-data-leakage-in-redirect)

**Entry point:** `/my-account?id=` — changing the id redirects, but the
response body leaks the target's data.

## Solution

1. `GET /my-account?id=carlos` with your session → 302 to `/`...
2. ...but the **response body** contains carlos's API key.
3. Submit the key — lab solved.

## Mitigation

Redirects still carry bodies — don't render sensitive data before the
authorization decision; discard the response entirely.
