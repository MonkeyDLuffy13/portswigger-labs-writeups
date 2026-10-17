# Lab 07 — Host validation bypass via connection state attack

> **Expert** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/lab-host-header-host-validation-bypass-via-connection-state-attack)

**Entry point:** Host validation happens per-request — but the back-end
connection is **reused across requests** (requires Burp ≥ 2022.8.1 features:
Repeater tab groups + "Send group in sequence (single connection)").

## Solution

1. Note `/admin` checks the Host **after** a first request has already been
   validated and opened a pooled back-end connection.
2. In Repeater, create a tab group with two requests sent in sequence on a
   **single connection**:
   - Request 1: ordinary `GET /` with the legitimate Host (validates, opens
     the back-end connection).
   - Request 2: `GET /admin` with an arbitrary/attacker Host — the front-end
     doesn't re-validate, and the already-established connection delivers
     it to the back-end.
3. The admin panel responds — delete carlos via
   `/admin/delete?username=carlos` — lab solved.

## Mitigation

Validate every request independently, and don't share validation state
across pooled connections; close/re-establish on Host mismatch.
