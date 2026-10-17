# Lab 08 — JWT authentication bypass via weak signing key

> **Practitioner** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-weak-signing-key)

**Entry point:** HS256 with a brute-forceable secret.

## Solution

1. Crack the secret with hashcat:

```bash
hashcat -a 0 -m 16500 <YOUR-JWT> /path/to/jwt.secrets.list
# re-run with --show to print again
```

→ secret is `secret1`.

2. JWT Editor → **New Symmetric Key** → replace `k` with
   `Base64("secret1")`.
3. Payload `sub: administrator`, **Sign** with the symmetric key ("Don't
   modify header") → `/admin` → delete carlos — lab solved.

## Mitigation

Enforce long random HMAC secrets (256-bit); rotate them; prefer asymmetric
algorithms with key pinning.
