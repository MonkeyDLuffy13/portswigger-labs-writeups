# Lab 10 — Unprotected admin functionality

> **Apprentice** · [Official lab](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality)

**Entry point:** `robots.txt` discloses the admin path.

## Solution

1. `GET /robots.txt` → `Disallow: /administrator-panel`.
2. Load `/administrator-panel` (no authentication at all) and delete
   `carlos` — lab solved.
