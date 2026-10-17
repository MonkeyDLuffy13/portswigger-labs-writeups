# Lab 06 — 2FA broken logic

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-broken-logic)

**Entry point:** `POST /login2` — the verification step trusts a
client-supplied cookie for the account.

## Solution

1. Log in as `wiener:peter`, complete 2FA, and note the flow: `POST /login`
   sets `verify=wiener` (cookie naming the account in the 2FA stage).
2. Request `GET /login2` with `verify=carlos`, then brute-force the 4-digit
   `mfa-code` with Burp Intruder (numbers 0000–9999, no concurrent
   requests).
3. The successful attempt returns **302** — follow it: you're in carlos's
   account — lab solved.

## Mitigation

The pre-auth session must not name the target account in a client-side
value; keep the identity server-side until 2FA completes.
