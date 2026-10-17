# Lab 02 — Stored XSS into HTML context with nothing encoded

> **Apprentice** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/stored)

**Entry point:** blog comment field — stored and rendered to every visitor.

## Solution

1. Open any blog post and post a comment containing:

```
<script>alert(1)</script>
```

2. The lab solves the moment the comment page re-renders (the alert fires for
   every viewer, since the payload is stored).

## Mitigation

Encode stored content on output; consider a strict sanitizer (DOMPurify) for
rich input.
