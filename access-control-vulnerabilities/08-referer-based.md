# Lab 08 — Referer-based access control

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-referer-based-access-control)

**Entry point:** `/admin-roles` authorization depends on the Referer
header (must be `/admin`).

## Solution

1. As admin, capture the upgrade request
   `POST /admin-roles` (`username=carlos&action=upgrade`).
2. As wiener, request `GET /admin-roles?username=carlos&action=upgrade`
   → denied (Referer absent).
3. In Repeater, replay with **wiener's cookie** and add:

```http
Referer: https://YOUR-LAB-ID.web-security-academy.net/admin
```

4. The upgrade succeeds — lab solved.

## Mitigation

Referer is client-controlled; authorize on the endpoint itself.
