# Lab 02 — Bypassing rate limits via race conditions

> **Expert** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-bypassing-rate-limits)

**Entry point:** the login rate limiter counts attempts per fixed window —
send the whole password list in **one parallel batch**.

## Solution

1. Capture `POST /login` (carlos + candidate password).
2. Duplicate the tab ~30 times (one per candidate password from the lab
   list), add all to a tab group, and send **in parallel** (single-packet
   attack) — the requests arrive within the same counting window, so the
   limit never triggers.
3. Check the responses: the request whose response isn't the rate-limit
   error is a hit — log in with that password — lab solved.

## Notes

Turbo Intruder's `engine.queue(..., gate=...)` does the same from a script.
