# Lab 12 — User ID controlled by request parameter with password disclosure

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-password-disclosure)

**Entry point:** `/my-account?id=` — the account page leaks the target's
password in the HTML source.

## Solution

1. `GET /my-account?id=administrator` with your session.
2. The response (view source) contains the administrator's password in an
   input field.
3. Log in as `administrator` and delete `carlos` — lab solved.
