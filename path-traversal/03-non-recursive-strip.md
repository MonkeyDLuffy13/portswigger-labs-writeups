# Lab 03 — Path traversal sequences stripped non-recursively

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-non-recursive-strip)

**Entry point:** `GET /image?filename=` · **Obstacle:** `../` is stripped —
but only **once**, non-recursively.

## Solution

1. `../../../etc/passwd` → becomes `/etc/passwd`... blocked/empty.
2. Nest the sequences so their removal creates new ones:

```
GET /image?filename=....//....//....//etc/passwd
```

The filter deletes `../` from each `....//` → the leftover is exactly
`../../../etc/passwd` — lab solved.

## Mitigation

Strip in a loop until the value stops changing (or simply allow-list the
expected filename).
