# Lab 06 — Web cache poisoning via an unkeyed query parameter

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-unkeyed-param)

**Entry point:** the cache key excludes UTM analytics parameters (`utm_*`)
— and `utm_content` is reflected.

## Solution

1. Confirm `GET /?utm_content=x` is reflected and still yields a cache hit
   for `/` (unkeyed).
2. Poison with a breakout payload:

```http
GET /?utm_content='><script>alert(1)</script>
```

3. Replay until `X-Cache: hit` with the payload stored, then keep the
   poisoned entry alive until the victim loads the home page — lab solved.

## Notes

UTM params are marketing junk — but sites that ignore them in the key often
still render them.
