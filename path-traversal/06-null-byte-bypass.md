# Lab 06 — File path traversal, validation of file extension with null byte bypass

> **Expert** · [Official lab](https://portswigger.net/web-security/file-path-traversal/lab-extension-filter-null-byte-bypass)

**Entry point:** `GET /image?filename=` · **Obstacle:** the filename **must
end with** `.png`.

## Solution

1. PHP (pre-5.3.4) truncates strings at a null byte — put the required
   extension **after** the path and a `%00`:

```
GET /image?filename=../../../etc/passwd%00.png
```

2. The filesystem receives `../../../etc/passwd\0` → reads `/etc/passwd` —
   lab solved.

## Notes

Null-byte truncation died in modern PHP/Java, but lives on in legacy stacks
and custom parsers — always test `%00` when an extension check blocks you.
