# Lab 13 — User ID controlled by request parameter

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)

**Entry point:** `/my-account?id=<username>` — straight IDOR.

## Solution

1. Log in, note `GET /my-account?id=wiener`.
2. Change to `GET /my-account?id=carlos` — his API key renders.
3. Submit the key — lab solved.

## Mitigation

Derive the identity from the session, never from a client-supplied id.
