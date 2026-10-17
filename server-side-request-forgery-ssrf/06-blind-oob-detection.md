# Lab 06 — Blind SSRF with out-of-band detection

> **Practitioner** · [Official lab](https://portswigger.net/web-security/ssrf/blind/lab-out-of-band-detection)

**Entry point:** the `Referer` header is requested server-side; the

> 🔧 **Burp Community alternative:** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
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
