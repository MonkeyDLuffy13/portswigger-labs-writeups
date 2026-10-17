# Lab 05 — Authentication bypass via information disclosure

> **Expert** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-authentication-bypass)

**Entry point:** a backup of a customized framework file reveals how
sessions are verified.

## Solution

1. `GET /robots.txt` → `Disallow: /backup`;
   `/backup/ProductTemplate.java.bak` leaks a customized
   framework class: the session is `base64(username + ':' + MD5(timestamp +
   SECRET_KEY))` — a **fixed** secret key.
2. Note the timestamp handling: the verification window is 60 seconds.
3. Request `GET /admin` with no session → 401; the response leaks the
   current server **timestamp** (date header + error details).
4. Craft your cookie for `administrator:MD5(current-timestamp + SECRET_KEY)`
   (script it so the timestamp is fresh), URL-encode, send to `/admin`.
5. Delete `carlos` — lab solved.

## Mitigation

Secrets in source/backups are compromised secrets — rotate and remove; use
server-side sessions.
