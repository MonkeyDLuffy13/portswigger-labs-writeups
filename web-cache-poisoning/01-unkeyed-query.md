# Lab 01 — Web cache poisoning (unkeyed query string)

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-unkeyed-query)

**Entry point:** the home page reflects query params, and the cache key
**excludes the query string**.

## Solution

1. Confirm the oracle: adding arbitrary params still yields `X-Cache: hit`
   → query is unkeyed.
2. Use a keyed header as a **cache buster** for your own testing:

```http
Origin: anything
```

3. Confirm reflection of params on cache misses, then poison:

```http
GET /?evil='/><script>alert(1)</script>
```

4. Replay until the response with the payload is served with `X-Cache: hit`.
5. Remove the `Origin` buster and keep replaying until ordinary users
   (`/` with no query) receive the poisoned entry — the victim's alert
   fires — lab solved.

## Notes

`Pragma: x-get-cache-key` reveals the cache key for debugging.
