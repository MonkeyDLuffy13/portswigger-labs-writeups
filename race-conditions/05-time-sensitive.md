# Lab 05 — Exploiting time-sensitive vulnerabilities

> **Expert** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-exploiting-time-sensitive-vulnerabilities)

**Entry point:** the reset token is `MD5(username + timestamp)` — two
parallel resets from **different sessions** that finish at the same
millisecond produce the **same token**.

## Solution

1. Confirm: PHP back-end serializes requests per session → use **two
   different sessions** (fresh cookie + CSRF from a cookie-less
   `GET /forgot-password`) and send both resets in parallel — responses
   align and two identical tokens arrive.
2. Token = `md5(username + timestamp)`. For carlos, brute-force the
   timestamp: request a reset for carlos and immediately test candidate
   timestamps (seconds-precision window) computing
   `md5('carlos' + str(t))` until the token matches the emailed format.
   (Script the candidates — Turbo Intruder or Python.)
3. Visit
   `/forgot-password?temp-forgot-password-token=<cracked>&username=carlos`? —
   use the reset flow with the predicted token, set a new password —
   lab solved.

## Notes

Time-based randomness = tiny keyspace. Predict, don't crack.
