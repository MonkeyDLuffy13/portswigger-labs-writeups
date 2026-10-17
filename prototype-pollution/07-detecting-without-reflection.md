# Lab 07 — Detecting server-side prototype pollution without polluted property reflection

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/server-side/lab-detecting-server-side-prototype-pollution-without-polluted-property-reflection)

**Entry point:** pollution isn't reflected — detect it via **status-code
override**.

## Solution

1. Break the JSON intentionally (remove a comma) → 500 with a JSON error
   body containing `"status": 400`.
2. Pollute + break simultaneously:

```json
"__proto__": {"status": 555},
...malformed...
```

3. The error body now reports **status 555** — your value was inherited by
   the error object from the polluted `Object.prototype` — server-side
   prototype pollution confirmed — lab solved.

## Notes

Other detection gadgets: `json spaces`, `charset` (Express body-parser
options) — any Express option works as a canary.
