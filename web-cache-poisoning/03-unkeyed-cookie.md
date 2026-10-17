# Lab 03 — Web cache poisoning with an unkeyed cookie

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-an-unkeyed-cookie)

**Entry point:** the `fehost` cookie is unkeyed and reflected inside a
double-quoted JavaScript string in the response.

## Solution

1. Load the home page — the first response sets `fehost=prod-cache-01`.
2. Reload: the cookie value is reflected inside
   `{"host":"prod-cache-01", ...}` in the body.
3. In Repeater, add a cache buster param, then break the JS string with the
   cookie:

```http
GET /?cachebuster=x HTTP/1.1
Cookie: fehost=someString"-alert(1)-"someString
```

4. Replay until `X-Cache: hit` with the payload in the body; verify in the
   browser that the alert fires.
5. Remove the buster and keep replaying until the victim's visit triggers
   the alert — lab solved.

## Mitigation

Cookies that influence output must be part of the cache key (or removed from
server-side logic entirely).
