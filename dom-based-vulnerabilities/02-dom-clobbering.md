# Lab 02 — DOM XSS exploiting DOM clobbering

> **Expert** · [Official lab](https://portswigger.net/web-security/dom-based/dom-clobbering/lab-dom-xss-exploiting-dom-clobbering)

**Entry point:** the comments script contains the clobberable pattern
`let defaultAvatar = window.defaultAvatar || {avatar: '/resources/images/avatarDefault.svg'}`
and later builds `<img ... src="defaultAvatar.avatar">`.

## Solution

1. Anchor elements become named properties of `window`; two anchors with the
   same `id` form a collection whose second member clobbers the `avatar`
   property via `name=avatar` + `href`.
2. Submit a comment containing the clobbering anchors (DOMPurify allows
   `cid:` and does **not** URL-encode double quotes):

```html
<a id=defaultAvatar><a id=defaultAvatar name=avatar href="cid:&quot;onerror=alert(1)//">
```

3. Submit a second, harmless comment. On the next render the app reads the
   clobbered `defaultAvatar.avatar` = `cid:"onerror=alert(1)//` and writes it
   into an `<img>` tag — the smuggled `onerror` executes — lab solved.
   (Chrome required.)

## Mitigation

Don't reference globals with `window.X || default` patterns for security-
relevant config; freeze config objects and validate IDs/attributes.
