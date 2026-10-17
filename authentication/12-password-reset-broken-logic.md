# Lab 12 — Password reset broken logic

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-broken-logic)

**Entry point:** `POST /forgot-password?temp-forgot-password-token=` — the
token is never actually validated on submission.

## Solution

1. Request a reset for your own account; note the flow: the token appears
   in the emailed URL, and the POST contains `username` as a hidden field.
2. In Repeater: **delete the token value** (URL + body) → the reset still
   works: the token is ignored.
3. Request a fresh reset (your account), then in Repeater blank the token
   and set `username=carlos`, with your chosen new password.
4. Log in as `carlos` with the new password — lab solved.

## Mitigation

The reset token must be validated server-side against the user and single-
use; never trust the hidden username field.
