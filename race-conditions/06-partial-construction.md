# Lab 06 — Partial construction race conditions

> **Expert** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-partial-construction)

**Entry point:** the confirmation email is constructed from **stale DB
data** while a parallel request mutates it — same gadget as the
single-endpoint lab; you may need to experiment to line up the window.

## Solution

1. Recon: email-change sends a confirmation containing the new address;
   submitting a second change invalidates the first link.
2. Build the tab group: one request setting the pending email to **your
   exploit-server address**, another setting it to **carlos's address** —
   send them in parallel (single-packet attack), tuning with warm-up
   requests until the confirmation email delivered to you is the one that
   **confirms carlos's pending change**.
3. Confirm it — carlos's account email becomes yours — then use the normal
   password reset on that address to take over the account — lab solved.

## Notes

"Partial construction": the email is rendered from data that another
request is concurrently rewriting.
