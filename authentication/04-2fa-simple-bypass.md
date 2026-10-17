# Lab 04 — 2FA simple bypass

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/multi-factor/2fa-simple-bypass)

**Entry point:** the session is already authenticated after the password
step — 2FA is just an extra page.

## Solution

1. `carlos:montoya` → `/login2` asks for the 4-digit code.
2. Skip it: the server already treats the session as logged-in — navigate
   straight to:

```
GET /my-account
```

Lab solved.

## Mitigation

Do not mark the session authenticated until **all** factors complete; keep
the pre-auth session scoped to the verification step only.
