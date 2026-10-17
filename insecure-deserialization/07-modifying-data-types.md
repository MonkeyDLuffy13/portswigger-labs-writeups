# Lab 07 — Modifying serialized data types

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-modifying-serialized-data-types)

**Entry point:** the signed session cookie compares a string token using
PHP's **loose comparison** (`==`) — PHP 7 semantics.

## Solution

1. Log in (`wiener:peter`) and decode the cookie: a `User` object with
   `username` (string) and `token` (string, must equal the server's secret
   access token).
2. PHP 7 loose comparison: `0 == "any non-numeric string"` is **true**.
   So change the token's type from string to **integer zero** — and set
   `username` to `carlos`:

```
O:4:"User":2:{s:12:"username";s:6:"carlos";s:5:"token";i:0;}
```

3. Re-encode as the session cookie, send `GET /my-account` — you're carlos.
4. `/admin` → delete carlos's account... (delete the user `carlos`) —
   lab solved.

## Mitigation

Use strict comparison (`===`) and consistent types; HMAC-sign the cookie.
