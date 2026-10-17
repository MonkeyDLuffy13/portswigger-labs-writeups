# Lab 03 — Forced OAuth profile linking

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/lab-oauth-forced-oauth-profile-linking)

**Entry point:** the "attach social profile" flow has **no `state`
parameter** — the final code-handoff is a simple GET you can force the
victim to make.

## Solution

1. Attach your own social profile; note the flow ends with
   `GET /oauth-linking?code=...` (no state).
2. Intercept your own `GET /oauth-linking?code=...` and **drop it** (keeps
   the code valid). Copy the URL.
3. Host the iframe on the exploit server:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/oauth-linking?code=STOLEN-CODE"></iframe>
```

4. Deliver to victim — their browser attaches **your** social profile to
   **their** admin account.
5. "Log in with social media" → you're the admin → delete carlos —
   lab solved.

## Mitigation

Always send and validate a `state` nonce in OAuth flows — it exists
precisely to stop forced-linking CSRF.
