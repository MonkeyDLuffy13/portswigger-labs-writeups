# Lab 07 — SSRF with whitelist-based input filter

> **Expert** · [Official lab](https://portswigger.net/web-security/ssrf/lab-ssrf-with-whitelist-filter)

**Entry point:** `stockApi` · **Obstacle:** the app parses the URL and
allow-lists only `stock.weliketoshop.net`.

## Solution

1. The parser supports **embedded credentials**:
   `http://username@stock.weliketoshop.net/` is accepted.
2. A `#` after the username would truncate the host — blocked as plaintext,
   but **double-URL-encoded** (`%2523`) it survives the filter and becomes
   `#` after decoding → server tries to connect to `username` (500 error
   proves it).
3. Final payload — credentials `localhost:80` + encoded fragment:

```
stockApi=http://localhost:80%2523@stock.weliketoshop.net/admin/delete?username=carlos
```

The server resolves `localhost:80/admin/delete?...` and deletes carlos —
lab solved.

## Mitigation

Allow-listing parsed URLs is defeated by credential/fragment tricks; pin the
resolved IP and reject anything unexpected after normalization.
