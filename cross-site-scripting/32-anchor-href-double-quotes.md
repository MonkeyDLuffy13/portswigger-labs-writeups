# Lab 32 — Stored XSS into anchor href attribute with double quotes HTML-encoded

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded)

**Entry point:** the comment "Website" field lands inside an `<a href>`.

## Solution

1. Post a comment with a website value; confirm it renders in the anchor's
   `href` (quotes are encoded, so no breakout — but the scheme is
   controllable).
2. Set the website to:

```
javascript:alert(1)
```

3. Click your (comment author) name on the post — the `javascript:` URL
   executes — lab solved.

## Mitigation

Allow-list URL schemes (`http`/`https` only) before writing user URLs into
href attributes.
