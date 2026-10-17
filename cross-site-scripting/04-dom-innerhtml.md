# Lab 04 — DOM XSS in innerHTML sink using source location.search

> **Apprentice** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/inner-html)

**Entry point:** blog search — the query is written into an `innerHTML` sink.

## Solution

1. Search something and inspect the page: the term lands in
   `element.innerHTML = ...` (no encoding).
2. `<script>` tags inserted via `innerHTML` do **not** execute — use an
   image error handler instead:

```
<img src=1 onerror=alert(1)>
```

3. Search with that payload — the alert fires — lab solved.

## Mitigation

Use `textContent` instead of `innerHTML` for untrusted data.
