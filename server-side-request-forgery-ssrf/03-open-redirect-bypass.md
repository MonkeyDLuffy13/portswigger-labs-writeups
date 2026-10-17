# Lab 03 — SSRF with filter bypass via an open redirect vulnerability

> **Expert** · [Official lab](https://portswigger.net/web-security/ssrf/ssrf-with-filter-bypass-via-open-redirect)

**Entry point:** `stockApi` — strictly allow-listed to
`stock.weliketoshop.net`.

## Solution

1. The allow-list is airtight on the host — so don't fight it. Find an open
   redirect **on the allowed host**:
   `/product/nextProduct?currentProductId=1&path=/product?productId=2`
   redirects (`302`) to `path`.
2. Point `stockApi` at the redirector and make `path` target the internal
   admin interface:

```
stockApi=/product/nextProduct?currentProductId=1&path=http://192.168.0.12/admin/delete?username=carlos
```

(URL-encode the nested `?`/`&` as needed: `%3f`, `%26`.)

3. The server fetches the allow-listed URL, receives `302 → 192.168.0.12/admin/...`,
   follows it, and deletes carlos — lab solved.

## Mitigation

An open redirect on an allow-listed host defeats the whole allow-list —
fix redirects there too, and pin resolved IPs.
