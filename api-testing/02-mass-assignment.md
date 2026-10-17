# Lab 02 — Exploiting a mass assignment vulnerability

> **Apprentice** · [Official lab](https://portswigger.net/web-security/api-testing/lab-exploiting-mass-assignment-vulnerability)

**Entry point:** `POST /api/checkout` — the GET response reveals a
`chosen_discount` field the POST doesn't send.

## Solution

1. Compare `GET` vs `POST /api/checkout` — the GET response's JSON includes
   `chosen_discount`.
2. Add it to the POST body (accepted = it's processed):

```json
{"chosen_discount":{"percentage":100},
 "chosen_products":[{"product_id":"1","quantity":1}]}
```

(Probe with `"x"` first — the type error proves input handling.)

3. 100% discount → buy the jacket — lab solved.

## Mitigation

Use allow-listed DTOs; never bind client JSON directly to internal objects.
