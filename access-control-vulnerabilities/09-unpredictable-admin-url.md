# Lab 09 — Unprotected admin functionality with unpredictable URL

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-unprotected-admin-functionality-with-unpredictable-url)

**Entry point:** the admin URL is unguessable — but disclosed in client JS.

## Solution

1. View the home page source: a script references the admin path, e.g.
   `/administrator-xxxxx-panel`.
2. Load it and delete `carlos` — lab solved.

## Mitigation

Security through obscurity is not access control; protect /admin with
authentication + authorization, and don't ship secrets to the client.
