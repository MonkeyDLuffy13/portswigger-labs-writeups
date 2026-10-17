# Lab 31 — Stored DOM XSS

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored)

**Entry point:** comments are rendered client-side; a `replace()` "filter"
encodes angle brackets — but replaces only the **first occurrence**.

## Solution

Post a comment with a sacrificial pair of angle brackets:

```
<><img src=1 onerror=alert(1)>
```

The `replace("<", "&lt;")` encodes the first `<><` sequence; the rest of
the payload survives into the DOM — lab solved.

## Notes

`String.replace` with a string argument is not global — with `/g` it would
still be insufficient for real sanitization.
