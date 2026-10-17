# Lab 05 — Exploiting exact-match cache rules for web cache deception

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-deception/lab-wcd-exploiting-exact-match-cache-rules)

**Entry point:** the cache has an **exact-match** rule for `/robots.txt`
(normalizing encoded dot-segments) — `/aaa/..%2frobots.txt` is cached as
`/robots.txt`.

## Solution

1. Fuzz delimiters: `;` and `?` work on the origin; neither yields caching.
2. `GET /robots.txt` → `X-Cache: miss` → resend → `hit` (exact-match rule).
3. `GET /aaa/..%2frobots.txt` → 200 **and cached** — the cache normalizes
   the dot-segment to the exact-match key.
4. The same normalization applies to authenticated pages: navigate the
   victim to `/aaa/..%2fmy-account` style paths (tune the segment so the
   origin resolves it to `/my-account` and the cache stores it under the
   pre-normalized key).
5. Request the stored URL — carlos's account data (CSRF token / API key) —
   lab solved.

## Mitigation

Normalize paths **before** applying cache rules; exact-match rules are only
safe if normalization can't smuggle other paths into them.
