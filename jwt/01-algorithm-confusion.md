# Lab 01 — JWT authentication bypass via algorithm confusion

> **Expert** · [Official lab](https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion)

**Entry point:** the server signs RS256 but **accepts HS256**, verifying it
with the *public* key (exposed at `/jwks.json`).

## Solution

1. Save the server's public key (X.509 PEM) from `/jwks.json`.
2. Derive the HMAC secret from it (Base64 of the DER form of the PEM) and
   create a **New Symmetric Key** in the JWT Editor extension, pasting that
   value into `k`.
3. In Repeater: set the JWT header `alg` to `HS256`, payload
   `sub: administrator`, **Sign** with your symmetric key
   ("Don't modify header").
4. `/admin` opens — delete carlos — lab solved.

## Mitigation

Reject tokens whose `alg` doesn't match the expected one; never feed
public keys into HMAC verification.
