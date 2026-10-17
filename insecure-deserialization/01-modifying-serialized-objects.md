# Lab 01 — Modifying serialized objects

> **Practitioner** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-objects)

**Entry point:** the `session` cookie is a Base64-encoded **serialized PHP
object** — and it is not signed.

## Solution

1. Log in (`wiener:peter`); in Burp Inspector decode the cookie:

```
O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:0;}
```

2. Flip the `admin` boolean to `b:1` (no length change needed) and re-encode.
3. Send `GET /my-account` with the modified cookie → the page now links to
   `/admin`.
4. Request `/admin`, then `/admin/delete?username=carlos` — lab solved.

## Mitigation

Sign serialized data (HMAC) — and better, don't deserialize user input at
all (use flat, opaque session tokens).
