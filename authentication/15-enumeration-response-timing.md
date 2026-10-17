# Lab 15 — Username enumeration via response timing

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-response-timing)

**Entry point:** passwords are rejected instantly for invalid usernames but
**hashed** for valid ones (timing oracle); IP block is bypassable via
`X-Forwarded-For`.

## Solution

1. Invalid username → immediate response. Valid username → the server
   hashes a long password first → ~seconds delay.
2. Intruder (sniper on `username`, fixed wrong password): add
   `X-Forwarded-For: §1§` as a second payload position with numbers 1–100
   (bypasses the IP block), sort responses by **time taken**.
3. The slow response = valid username.
4. Second attack: that username × password list, same X-Forwarded-For
   rotation — one response is **302**.
5. Log in as the victim — lab solved.

## Notes

Hash a dummy string for *every* login attempt to flatten timing.
