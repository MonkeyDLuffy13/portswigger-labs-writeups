# Lab 06 — Bypassing flawed input filters for server-side prototype pollution

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/server-side/lab-bypassing-flawed-input-filters-for-server-side-prototype-pollution)

**Entry point:** `__proto__` is blocked in the JSON — use the
`constructor.prototype` alias (Node.js).

## Solution

1. `POST /my-account/change-address` accepts JSON and reflects the user
   object.
2. `"__proto__":{"json spaces":10}` → no effect (blocked). Try:

```json
"constructor": {"prototype": {"json spaces": 10}}
```

→ the response JSON becomes indented by 10 spaces — prototype polluted
(Express `JSON.stringify` reads `json spaces` from the prototype).

3. Escalate — the reflected user has `"isAdmin": false` and no own property:

```json
"constructor": {"prototype": {"isAdmin": true}}
```

4. Refresh — the admin-panel link appears; delete `carlos` — lab solved.
