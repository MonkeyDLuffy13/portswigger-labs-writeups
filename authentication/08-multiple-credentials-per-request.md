# Lab 08 — Broken brute-force protection, multiple credentials per request

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-broken-brute-force-protection-multiple-credentials-per-request)

**Entry point:** `POST /login` accepts JSON — and arrays.

## Solution

1. Change `password` from a string to an **array** of all candidates:

```json
{"username":"carlos","password":["123456","password","qwerty","..."]}
```

2. One request tries every password; the response is **302**.
3. Right-click → *Show response in browser* → open it → My account —
   lab solved.

## Notes

Type juggling: validation code expecting a string silently iterates arrays.
Enforce types on every input.
