# Lab 06 — JWT authentication bypass via kid header path traversal

> **Practitioner** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-kid-header-path-traversal)

**Entry point:** the `kid` header is used to build a filesystem path for
the verification key — traverse it to a predictable file.

## Solution

1. JWT Editor → **New Symmetric Key** → generate, then replace `k` with an
   **empty string** (the "key" will be the empty `/dev/null` contents).
2. In Repeater's JWT tab: set `kid` to
   `../../../../../../../dev/null`, payload `sub: administrator`, **Sign**
   with the symmetric key ("Don't modify header").
3. The server loads `/dev/null` (empty) as the HMAC secret = your empty key
   — signature valid → `/admin` → delete carlos — lab solved.

## Mitigation

Never build key paths from the `kid`; treat it as an opaque index into a
server-side map.
