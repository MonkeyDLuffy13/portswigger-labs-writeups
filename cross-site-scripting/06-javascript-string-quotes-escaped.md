# Lab 06 — Reflected XSS into a JavaScript string with single quote and backslash escaped

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/javascript-string)

**Entry point:** `GET /?search=` — reflected inside a JavaScript string
literal; `'` and `\` are backslash-escaped.

## Solution

1. Confirm the context: the response contains `var searchTerms = 'test';`
   and `'` becomes `\'`.
2. Quotes are useless, but the payload still sits inside a `<script>` block —
   close the tag itself:

```
</script><script>alert(1)</script>
```

3. The first closing tag terminates the original script; the injected one
   executes — lab solved.

## Mitigation

Escaping quotes only protects string context. Encode `<`/`>` too, or move
data out of inline scripts entirely.
