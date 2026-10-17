# Lab 05 — JWT authentication bypass via jwk header injection

> **Expert** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-jwk-header-injection)

**Entry point:** the JWT embeds its own verification key in the `jwk`
header — and the server trusts it.

## Solution

1. JWT Editor → **New RSA Key** → generate.
2. In Repeater's JWT tab: set `sub: administrator`, click **Attack →
   Embedded JWK**, choose your key — the extension adds your public key as
   the `jwk` header and signs the token with the matching private key.
3. `/admin` → delete carlos — lab solved.

(Manual alternative: add the `jwk` header yourself and match `kid`.)

## Mitigation

Never read verification keys from the token; use a fixed server-side key
per `kid`.
