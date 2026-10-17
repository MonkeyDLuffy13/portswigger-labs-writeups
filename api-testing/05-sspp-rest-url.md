# Lab 05 — Exploiting server-side parameter pollution in a REST URL

> **Practitioner** · [Official lab](https://portswigger.net/web-security/api-testing/server-side-parameter-pollution/lab-exploiting-server-side-parameter-pollution-in-rest-url)

**Entry point:** `username` is placed into a server-side **URL path**
unescaped.

## Solution

1. Probe: `administrator%23` → *"Invalid route"* (fragment truncates the
   path); `administrator%3F` → same (query start); `../administrator` →
   normal response (relative path works).
2. Climb out with `../` until *"Not found"* (`../../../../%23` = outside the
   API root).
3. At that level, probe for an API definition:

```
username=../../../../openapi.json%23
```

→ the OpenAPI document reveals the user-lookup endpoint
(`/api/int`-style internal route) — lab solved.

## Notes

REST-path pollution = path traversal inside the server's own API calls;
use fragments (`#`) to cut the trailing suffix and `../` to explore.
