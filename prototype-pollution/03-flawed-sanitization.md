# Lab 03 — Client-side prototype pollution via flawed sanitization

> **Practitioner** · [Official lab](https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-client-side-prototype-pollution-via-flawed-sanitization)

**Entry point:** a blocklist sanitizer strips `__proto__`/`constructor`/
`prototype` — but **non-recursively**; nested keys re-form them.

## Solution

1. Classic vectors (`__proto__[foo]`, `constructor.prototype.foo`) are
   stripped.
2. Bypass by nesting so sanitization rebuilds the dangerous key:

```
/?__pro__proto__to__[transport_url]=data:,alert(1);
```

(removing the inner `__proto__` from `__pro__proto__to__` leaves
`__proto__`).

3. The gadget (`searchLogger.js`) appends a script from the polluted
   `transport_url` → the `data:` URL executes — lab solved.
