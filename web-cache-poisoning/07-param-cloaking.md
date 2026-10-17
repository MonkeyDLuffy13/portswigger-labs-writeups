# Lab 07 — Web cache poisoning: parameter cloaking

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-param-cloaking)

**Entry point:** JSONP import `/js/geolocate.js?callback=setCountryCookie`;
UTM params are excluded from the cache key; the server accepts `;` as a
parameter separator (the cache does not).

## Solution

1. Confirm duplicate-parameter handling: send a **fat-body duplicate**
   `callback` — the app uses the body's value while the cache keys on the
   query-string value.
2. Cloak the override behind the excluded UTM param with a `;` separator:

```http
GET /js/geolocate.js?callback=setCountryCookie&utm_content=foo;callback=alert(1) HTTP/1.1
```

3. The cache keys on `callback=setCountryCookie` (first value), but the
   server parses `;` and uses the last `callback=alert(1)` — the cached
   JSONP now calls `alert(1)`.
4. Remove nothing (the key already matches the victim's import) — the
   victim's page imports the poisoned resource — lab solved.

## Mitigation

Align parameter parsing between cache and origin; reject `;`-separated
parameters.
