# Lab 03 — Username enumeration via subtly different responses

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-subtly-different-responses)

**Entry point:** `POST /login` — error messages are identical, but subtle
differences remain (dot placement, response length).

## Solution

1. All failures return the same message... except one candidate's response
   has **one extra character** (a trailing period).
2. Intruder (sniper on `username`) → sort responses by length → the outlier
   is the valid account.
3. Same for `password`: brute-force with the valid username; here the
   correct password returns a subtly different response **plus a 302**.
   Use "Grep - Extract" on the response body to spot the difference.
4. Log in as the victim — lab solved.

## Notes

When messages look identical, diff **bytes and headers**, not words —
a single dot is enough to enumerate.
