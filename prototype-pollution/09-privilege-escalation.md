# Lab 09 — Privilege escalation via server-side prototype pollution

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/server-side/lab-privilege-escalation-via-server-side-prototype-pollution)

**Entry point:** the reflected user object inherits `isAdmin` from the
prototype — pollute it true.

## Solution

1. Confirm the source: `"__proto__":{"foo":"bar"}` → the response object
   now includes `foo` (inherited).
2. Escalate:

```json
"__proto__": {"isAdmin": true}
```

3. The response flips `isAdmin` to true; refresh the page — the admin-panel
   link appears — delete `carlos` — lab solved.
