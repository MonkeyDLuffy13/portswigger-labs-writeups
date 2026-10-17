# Lab 33 — Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-onclick-event-angle-brackets-double-quotes-html-encoded-single-quotes-backslash-escaped)

**Entry point:** the "Website" field lands inside an
`onclick="...location='...'"` handler — quotes/backslashes escaped, angle
brackets encoded. HTML entities inside `onclick` are **HTML-decoded before
JS parsing** — use `&apos;`.

## Solution

1. Set the website value to:

```
http://foo?&apos;-alert(1)-&apos;
```

2. The page HTML-decodes `&apos;` to `'` *after* attribute parsing, so the
   onclick JS sees unescaped quotes:
   `location='http://foo?&#39;-alert(1)-&#39;'` → runs
   `'-alert(1)-'` — clicking your name fires the alert — lab solved.

## Notes

Escape order matters: attribute-value decoding happens before the JS
parser, so HTML entities are a quote-escaping bypass inside event handlers.
