# Lab 13 — Web cache poisoning: URL normalization

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-normalization)

**Entry point:** the cache **URL-decodes** the request line before caching,
while browsers encode it — the key mismatch lets encoded XSS land decoded
in the cache.

## Solution

1. `GET /random</p><script>alert(1)</script><p>foo` — the path is reflected
   into the error page; but browsing that URL yourself doesn't fire (the
   browser sends it percent-encoded).
2. Poison in Repeater with the raw (decoded) payload, then immediately load
   the encoded URL in the browser — the cache decodes your request, so the
   browser's encoded request keys to the same entry and receives the
   decoded, executing payload.
3. Re-poison and click **Deliver link to victim** — their visit executes
   the alert — lab solved.

## Notes

Any normalization gap between cache and client (decoding, dot-segments,
backslashes) is cache-key confusion you can poison through.
