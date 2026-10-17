# Lab 04 — DOM XSS via an alternative prototype pollution vector

> **Practitioner** · [Official lab](https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-dom-xss-via-an-alternative-prototype-pollution-vector)

**Entry point:** the same `transport_url` gadget, but reached via an
alternative vector — and mind the **XSS context** after injection.

## Solution

1. The hash-based source works; use `constructor` instead of `__proto__`
   and adjust the payload so the injected JS stays syntactically valid in
   the sink's context:

```
/#constructor[prototype][transport_url]=foo
```

2. Tune the payload for the context (per the lab hint), e.g.:

```
/#constructor[prototype][transport_url]=data:,alert(1);
```

The alert fires — lab solved.
