# Lab 04 — Method-based access control

> **Apprentice** · [Official lab](https://portswigger.net/web-security/access-control/lab-method-based-access-control)

**Entry point:** `POST /admin-roles` — authorization enforced only on POST.

## Solution

1. Admin demo (`administrator:admin`) upgrades users via
   `POST /admin-roles` (`username=carlos&action=upgrade`). Save the request.
2. Log in as `wiener:peter` in another session.
3. Replay the upgrade request with **wiener's session cookie**, changing the
   method to **GET** and moving parameters to the query string:

```
GET /admin-roles?username=wiener&action=upgrade HTTP/1.1
```

4. The GET variant skips the authorization check — wiener becomes admin —
   lab solved.

## Mitigation

Enforce authorization on the **resource and action**, not on the HTTP method;
never let the method select the code path.
