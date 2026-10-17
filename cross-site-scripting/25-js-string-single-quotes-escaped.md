# Lab 25 — Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-double-quotes-encoded-single-quotes-escaped)

**Entry point:** `?search=` inside a JS string; `'` → `\'` but the
**backslash itself is not escaped**.

## Solution

Escape the escaper, then break out:

```
\'-alert(1)//
```

The response yields `...\\'-alert(1)//` — the injected backslash neutralizes
the added one, the quote closes the string, and `//` comments the tail —
lab solved.

## Notes

Whenever `'` is escaped with `\`, always test `\` — if it passes through,
the whole escaping scheme collapses.
