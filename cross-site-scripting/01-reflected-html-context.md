# Lab 01 — Reflected XSS into HTML context with nothing encoded

> **Apprentice** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/reflected)

**Entry point:** `GET /?search=` — reflected verbatim into the results page.

## Solution

1. Type anything in the search box and note the reflection:
   `<span class="...">test</span>` — no encoding at all.
2. Inject a classic script tag:

```
<script>alert(1)</script>
```

3. The alert fires — lab solved.

## Mitigation

HTML-encode untrusted output (`<` `>` `&` `"`) in HTML context.
