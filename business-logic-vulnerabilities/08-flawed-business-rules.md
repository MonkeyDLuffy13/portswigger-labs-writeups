# Lab 08 — Flawed enforcement of business rules

> **Practitioner** · [Official lab](https://portswigger.net/web-security/logic-flaws/flawed-enforcement-of-business-rules)

**Entry point:** two coupons (`NEWCUST5`, `SIGNUP30`) — "already applied"
is checked only for **consecutive** duplicates.

## Solution

1. Collect both codes (account page + newsletter signup).
2. Apply them to the leather jacket alternating:

```
NEWCUST5, SIGNUP30, NEWCUST5, SIGNUP30, ...
```

The rule rejects the *same code twice in a row*, so alternation re-applies
both indefinitely.

3. Reduce the total below your store credit and checkout — lab solved.

## Mitigation

Track applied coupon IDs per order globally — not just the last one.
