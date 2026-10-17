# Lab 01 — User role controlled by request parameter

> **Apprentice** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-role-controlled-by-request-parameter)

**Entry point:** session cookie holds the role.

## Solution

1. Log in as `wiener:peter`, decode the `session` cookie (Base64):

```json
{"username":"wiener","role":"default"}
```

2. Flip the role and re-encode:

```json
{"username":"wiener","role":"administrator"}
```

3. Set it back in the cookie, load `/admin`, and delete `carlos` —
   lab solved.

## Mitigation

Never store authorization data client-side; keep roles server-side, keyed by
an opaque session ID.
