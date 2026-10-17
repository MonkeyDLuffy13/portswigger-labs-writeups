# Lab 10 — Reflected XSS into a template literal with angle brackets, single, double quotes, and backslash escaped

> **Expert** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/template-literal)

**Entry point:** `GET /?search=` — reflected inside a **backtick template
literal**; quotes and backslashes are escaped.

## Solution

1. Note the reflection inside ``var message = `search term`; ``. Escaping
   covers `'` `"` `\` but **not backticks or `${ }`**.
2. Inject a template substitution that calls `alert`:

```
${alert(1)}
```

Resulting code evaluates the substitution at render time — the alert fires —
lab solved.

## Mitigation

Unicode-escape backticks and `$` in template literals, or stop interpolating
raw input into inline JavaScript.
