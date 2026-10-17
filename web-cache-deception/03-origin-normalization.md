# Lab 03 — Exploiting origin server normalization for web cache deception

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-origin-server-normalization)

**Entry point:** the **origin** decodes and resolves encoded dot-segments
(`/aaa/..%2fmy-account` → `/my-account`) while the cache keys the literal
path.

## Solution

1. Confirm: `GET /aaa/..%2fmy-account` → 200 with your API key.
2. Static resources live under `/resources` and are cached; the cache
   normalizes `/resources/..%2fX` to `/X` too, but the origin's
   normalization wins for the response while the cache stores it under the
   `/resources/...` key (static rule).
3. Craft the victim navigation with the traversal + `.js` suffix:

```html
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/resources/..%2fmy-account/wcd.js"</script>
```

(tune: `X-Cache: miss` → victim request → `hit` for your replay).

4. Request the same URL — carlos's API key — submit it — lab solved.
