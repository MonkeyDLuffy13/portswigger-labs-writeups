# Lab 06 — Blind SSRF with out-of-band detection

> **Practitioner** · [Official lab](https://portswigger.net/web-security/ssrf/blind/lab-out-of-band-detection)

**Entry point:** the `Referer` header is requested server-side; the
application shows no response difference.

## Solution

1. In Repeater, replace the `Referer` domain with a **Burp Collaborator**
   payload (right-click → *Insert Collaborator Payload*):

```http
Referer: https://YOUR-COLLABORATOR-SUBDOMAIN
```

2. Send — **Poll now** shows DNS/HTTP interactions initiated by the
   application — blind SSRF confirmed — lab solved.

## Notes

When blind, always fuzz *every* header with Collaborator payloads
(Collaborator Everywhere automates this).
