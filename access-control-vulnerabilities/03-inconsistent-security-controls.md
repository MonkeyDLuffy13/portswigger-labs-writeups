# Lab 03 — Access control vulnerabilities: inconsistent security controls

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-inconsistent-security-controls)

**Entry point:** user registration vs email-change use different validation.

## Solution

1. Register normally — the site rejects `@dontwannacry.com` addresses
   (employee domain) at signup.
2. But **email change** accepts any domain: change your email to
   `attacker@dontwannacry.com` — you're now treated as staff.
3. `/admin` becomes accessible; delete `carlos` — lab solved.

## Notes

Authorization decisions derived from mutable user attributes (email domain)
must be re-validated consistently at every entry point.
