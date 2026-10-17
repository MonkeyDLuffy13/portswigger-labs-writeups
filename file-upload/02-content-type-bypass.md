# Lab 02 — Web shell upload via Content-Type restriction bypass

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-content-type-restriction-bypass)

**Entry point:** the upload validates only the multipart part's
`Content-Type`.

## Solution

1. Upload `exploit.php` → rejected (needs `image/jpeg`/`image/png`).
2. In Repeater, replay the upload with the PHP content but set the file
   part's `Content-Type: image/jpeg`.
3. `GET /files/avatars/exploit.php` executes — submit the secret —
   lab solved.
