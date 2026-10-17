# Lab 21 — Exploiting XSS to bypass CSRF defenses

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-perform-csrf)

**Entry point:** the email form has a CSRF token — but stored comments
render above it and allow `<input>` tags.

## Solution

1. Post a comment injecting a **hidden input that matches the email
   field's name** — the browser takes the first match:

```html
<input type="hidden" name="email" value="hacked@evil-you.net">
```

2. When the victim submits their own (token-valid) form, the injected value
   is sent instead of theirs — their email changes — lab solved.

## Notes

XSS beats CSRF tokens: with script injection you could also steal/submit
the token directly; here a name-collision input is enough.
