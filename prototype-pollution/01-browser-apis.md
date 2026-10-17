# Lab 01 — Client-side prototype pollution via browser APIs

> **Practitioner** · [Official lab](https://portswigger.net/web-security/prototype-pollution/client-side/browser-apis/lab-prototype-pollution-client-side-prototype-pollution-via-browser-apis)

**Entry point:** `?__proto__[foo]=bar` pollutes `Object.prototype`; the
gadget uses `Object.defineProperty` on `transport_url` **without a value**
— so a polluted `value` property fills the gap.

## Solution

1. Confirm the source: `/?__proto__[foo]=bar` → `Object.prototype.foo = "bar"`.
2. Gadget: `searchLoggerConfigurable.js` appends a script from
   `config.transport_url`, defined via `defineProperty` with
   `writable:false, configurable:false` but **no value**.
3. Exploit:

```
/?__proto__[value]=data:,alert(1);
```

The polluted `value` supplies the missing property → script src =
`data:,alert(1);` — lab solved.
