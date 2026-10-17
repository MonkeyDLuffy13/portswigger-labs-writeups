# Lab 27 — Reflected XSS protected by CSP, with CSP bypass

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-csp-bypass)

**Entry point:** the CSP `report-uri` directive contains a `token` parameter
that is **reflected back into the policy itself**.

## Solution

1. Normal payloads reflect but don't execute — the CSP blocks inline
   scripts.
2. Inject a new directive through the token:

```
/?search=<script>alert(1)</script>&token=;script-src-elem 'unsafe-inline'
```

(URL-encoded; the leading `;` terminates the previous directive.)

3. `script-src-elem 'unsafe-inline'` overrides the script restriction for
   `<script>` elements — the inline alert runs — lab solved.

## Notes

CSP injection: any user input concatenated into the policy header is a
policy override primitive.
