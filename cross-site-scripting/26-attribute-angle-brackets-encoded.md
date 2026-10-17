# Lab 26 — Reflected XSS into attribute with angle brackets HTML-encoded

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-attribute-angle-brackets-encoded)

**Entry point:** `?search=` reflected inside a tag attribute; `<`/`>`
encoded — so stay inside the attribute and close it.

## Solution

```
"onmouseover="alert(1)
```

URL-encoded: `%22onmouseover%3D%22alert(1)`

The attribute closes early; `onmouseover` becomes a new attribute on the
same tag — hover over the injected text to fire it. (This lab requires the
victim — deliver the URL via the exploit server so their cursor triggers
it — lab solved.)
