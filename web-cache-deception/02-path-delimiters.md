# Lab 02 — Exploiting path delimiters for web cache deception

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-path-delimiters)

**Entry point:** the origin uses `;` and `?` as **path delimiters**
(`/my-account;foo` serves `/my-account`); the cache doesn't treat `;` as a
delimiter and caches `.js` URLs.

## Solution

1. Intruder-fuzz `/my-account§§abc` → `;` and `?` return 200 with your API
   key (delimiters).
2. Cache check: `/my-account?abc.js` → not cached (cache uses `?` too), but
   `/my-account;abc.js` → `X-Cache: miss` then **hit** — cache keys the full
   path as static JS.
3. Deliver the navigation payload (fresh segment for the victim):

```html
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account;wcd.js"</script>
```

4. Request the same URL — carlos's API key is in the cached response —
   submit it — lab solved.
