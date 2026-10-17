# Lab 11 — SameSite Strict bypass via sibling domain

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-sibling-domain)

**Entry point:** the chat WebSocket (`/chat`) is CSRF-able but the session

> 🔧 **Burp Community alternative:** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
cookie is `SameSite=Strict` — until you find the **sibling domain** with XSS.

## Solution

1. Confirm the CSWSH fails cross-site (Strict blocks the cookie).
2. Find the sibling: responses for the site's scripts/images carry
   `Access-Control-Allow-Origin: https://cms-YOUR-LAB-ID.web-security-academy.net`
   — a same-site sibling hosting a CMS login form with **reflected XSS** in
   `username` (works via GET too).
3. URL-encode the CSWSH script and deliver it through the sibling XSS
   (redirector on the exploit server):

```html
<script>
document.location = "https://cms-YOUR-LAB-ID.web-security-academy.net/login?username=URL-ENCODED-CSWSH-SCRIPT&password=x";
</script>
```

where the encoded script is the WebSocket hijacker from the websockets labs
(opens `wss://YOUR-LAB-ID/chat`, sends `READY`, POSTs `event.data` to your
Collaborator).

4. Deliver to victim — the XSS runs on the sibling domain (same **site** →
   Strict cookie attached) — Collaborator receives the victim's chat
   history including their credentials — log in as carlos — lab solved.

## Mitigation

"Same-site" includes every sibling subdomain: one XSS anywhere on a sibling
defeats SameSite=Strict. Segment trust accordingly.
