# Lab 03 — Source code disclosure via backup files

> **Apprentice** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-via-backup-files)

**Entry point:** `/robots.txt` reveals a hidden `/backup` directory.

## Solution

1. `GET /robots.txt` → `Disallow: /backup`.
2. `GET /backup` → lists `ProductTemplate.java.bak`.
3. `GET /backup/ProductTemplate.java.bak` → the Java source contains a
   hard-coded **Postgres database password**.
4. Submit the password — lab solved.

## Mitigation

Never leave backup/editor artifacts in web roots; deny access to non-app
paths and scrub secrets from source.
