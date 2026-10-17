# Lab 03 — JWT authentication bypass via flawed signature verification

> **Practitioner** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-flawed-signature-verification)

**Entry point:** the server accepts the `none` algorithm.

## Solution

1. Decode the session JWT: `sub` holds the username.
2. Set `sub: administrator`; set the header `alg` to **`none`**; delete the
   signature (keep the trailing dot after the payload):

```
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzdWIiOiJhZG1pbmlzdHJhdG9yIn0.
```

3. `/admin` opens — delete carlos — lab solved.
