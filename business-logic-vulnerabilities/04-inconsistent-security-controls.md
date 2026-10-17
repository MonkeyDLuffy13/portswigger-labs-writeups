# Lab 04 — Inconsistent security controls

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/inconsistent-security-controls)

**Entry point:** the admin panel is restricted to `@dontwannacry.com` emails
— but the email-change form doesn't enforce the domain.

## Solution

1. Discover `/admin` with Burp *Engagement tools → Discover content*.
2. Visiting it reveals only `@dontwannacry.com` users get access.
3. Register normally using your own lab email domain (from the **Email
   client** button); confirm via the mailed link.
4. My account → change email to **any address at `@dontwannacry.com`** —
   the change succeeds.
5. `/admin` now loads; delete `carlos` — lab solved.

## Notes

The flaw is consistency: strict validation at registration, none at
email-change, while authorization depends on the email domain.
