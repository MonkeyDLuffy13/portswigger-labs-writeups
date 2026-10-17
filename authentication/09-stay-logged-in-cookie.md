# Lab 09 — Brute-forcing a stay-logged-in cookie

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-brute-forcing-a-stay-logged-in-cookie)

**Entry point:** `stay-logged-in` cookie =
`base64(username + ':' + md5(password))` — offline brute-forceable.

## Solution

1. Log in with *Stay logged in*; decode the cookie: `wiener:51dc30dd...` —
   MD5 of your password. Format confirmed.
2. Intruder on a `GET /my-account?id=carlos` request, payload position on
   the `stay-logged-in` cookie, payloads = candidate passwords.
3. Payload processing rules (in order): **MD5 hash** → **add prefix
   `carlos:`** → **Base64-encode**.
4. Grep-match on `Update email` (only visible when authenticated). Run.
5. The single flagged request reveals carlos's password — log in —
   lab solved.

## Mitigation

Don't put credentials (even hashed) in cookies; use server-side session
tokens with secure random values.
