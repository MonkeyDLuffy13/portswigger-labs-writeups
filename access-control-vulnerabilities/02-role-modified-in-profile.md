# Lab 02 — User role can be modified in user profile

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-role-can-be-modified-in-user-profile)

**Entry point:** the email-change response leaks internal user data.

## Solution

1. `wiener:peter` → change email and inspect the response: it echoes the
   full user JSON, including `"roleid": 1`.
2. Re-send the email change with an added field:

```json
{"email":"wiener@normal-user.net","roleid":2}
```

3. The role is updated server-side. Load `/admin` and delete `carlos` —
   lab solved.

## Notes

Mass-assignment: the update handler copies every JSON key into the object.
Reject unknown fields explicitly.
