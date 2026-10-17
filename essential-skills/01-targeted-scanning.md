# Lab 01 — Discovering vulnerabilities quickly with targeted scanning

> **Practitioner** · [Official lab](https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing/lab-discovering-vulnerabilities-quickly-with-targeted-scanning)

**Entry point:** use Burp Scanner's **audit of a selected insertion point**
to find a vulnerability fast.

## Solution

1. Log in; capture `GET /my-account?id=wiener` (session cookie contains
   `wiener:<token>`).
2. In Repeater, select the cookie's insertion point → right-click →
   **Scan selected insertion point** → OK (Pro feature — see note).
3. Dashboard → the audit reports a **Stored XSS** within ~a minute.
4. Open the issue's request, send it to Repeater, replace the scanner's PoC
   with a real exfiltration payload, send, and confirm the issue —
   lab solved.

> 🔧 **Burp Community alternative:** active auditing is Pro-only. Do it
> manually: swap the cookie's token part for `'"><svg/onload=...>`-style
> payloads (the cookie is reflected into a comment form field) until the
> stored XSS fires for other visitors.

## Mitigation

Treat cookie/token values as untrusted input everywhere they're rendered.
