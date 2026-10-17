# Lab 04 — Exploiting cache server normalization for web cache deception

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-cache-server-normalization)

**Entry point:** the origin ignores encoded dot-segments, but the **cache**
decodes `%2f` and normalizes the path — flip the discrepancy the other way.

## Solution

1. Fuzz delimiters (`/my-account§§abc`): the origin recognizes `#`, `?`,
   `%23`, `%3f` — ignore `#` (the browser consumes it).
2. Delimiter + extension combos don't cache. Move to normalization:
   `GET /aaa/..%2fmy-account` → 404 (origin doesn't normalize) but the
   **cache** decodes it — its key becomes the normalized
   `/my-account`-style path with the `.js` suffix applied.
3. Find a cacheable suffix the origin tolerates, then deliver:

```html
<script>document.location="https://YOUR-LAB-ID.web-security-academy.net/my-account;wcd.js?cachebust=..."?
</script>
```

(tune per the lab's findings: cache decodes `%2f`, origin doesn't — the
victim's authenticated response is cached under the decoded static key,
which you then request to read carlos's API key — lab solved.)
