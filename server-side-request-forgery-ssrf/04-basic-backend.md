# Lab 04 — Basic SSRF against another back-end system

> **Practitioner** · [Official lab](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-backend-system)

**Entry point:** `stockApi` · the admin panel lives on an **internal**
back-end at `192.168.0.x:8080`.

## Solution

1. Set `stockApi=http://192.168.0.1:8080/admin`, mark the final octet as an
   Intruder payload (Numbers 1–255, step 1).
2. Sort by status — one request returns **200**: the admin interface (e.g.
   `192.168.0.13`).
3. Send it to Repeater and delete the user:

```
stockApi=http://192.168.0.13:8080/admin/delete?username=carlos
```

Lab solved.

## Notes

SSRF + internal network scan: enumerate private ranges through the SSRF
primitive when the target isn't on localhost.
