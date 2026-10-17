# Lab 05 — File path traversal, validation of start of path

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-validation-of-start-of-path)

**Entry point:** `GET /image?filename=` · **Obstacle:** the value **must
start with** the expected base folder (`/var/www/images/`).

## Solution

1. The check only verifies the prefix — traversal after it is untouched:

```
GET /image?filename=/var/www/images/../../../etc/passwd
```

Lab solved.

## Notes

"Starts with" is a start, not a validation. Canonicalize the joined path and
confirm it is still inside the intended directory.
