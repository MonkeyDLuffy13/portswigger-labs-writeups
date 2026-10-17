# Lab 04 — JWT authentication bypass via jku header injection

> **Expert** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jku-header-injection)

**Entry point:** the JWT `jku` header tells the server where to fetch the
verification key (JWK Set) — point it at your own.

## Solution

1. JWT Editor → **New RSA Key** → generate.
2. Host a JWK Set on the exploit server containing your public key:

```json
{"keys": [{"kty": "RSA", "e": "AQAB", "kid": "<YOUR-KID>",
           "n": "<YOUR-MODULUS>"}]}
```

3. In Repeater's JWT tab: set `kid` to your key's kid, add
   `jku: https://YOUR-EXPLOIT-SERVER/jwks.json`, set `sub: administrator`,
   **Sign** with your RSA key ("Don't modify header").
4. `/admin` → delete carlos — lab solved.

## Mitigation

Match the `jku`/`kid` against a fixed allow-list of key sources; never
fetch keys from user-controlled URLs.
