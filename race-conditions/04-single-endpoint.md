# Lab 04 — Single-endpoint race conditions

> **Expert** · [Official lab](https://portswigger.net/web-security/race-conditions/lab-race-conditions-single-endpoint)

**Entry point:** `POST /my-account/change-email` — one pending email is
stored per account; parallel requests collide between the email-sending
task and the DB update.

## Solution

1. Duplicate the change-email request ~20×, each with a **unique**
   `@YOUR-EXPLOIT-SERVER.exploit-server.net` address, in one tab group.
2. Send **in parallel**: some confirmation emails arrive whose recipient
   doesn't match the pending address stored at the time they were rendered.
3. The known finish: race one request with `email=carlos@ginandjuice.shop`
   (the admin's address) together with your exploit-server addresses — the
   confirmation email delivered **to you** contains the token that confirms
   carlos's address — then reset carlos's password via "Forgot password"
   and log in as carlos — lab solved.

## Mitigation

Store the pending email keyed to a token generated **after** the DB write;
use unique constraints and atomic compare-and-swap updates.
