# Lab 23 — Web cache poisoning via HTTP/2 request tunnelling

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-web-cache-poisoning-via-request-tunnelling)

**Entry point:** tunnel a request inside `:path` (HTTP/2) via a `Host`
header + blank line, and capture the front-end's rewritten suffix with a
trailing arbitrary header.

## Solution

1. Confirm tunnelling (HTTP/2, Inspector → Request Attributes = HTTP/2):

```
:path: /?cachebuster=2 HTTP/1.1\r\nHost: YOUR-LAB-ID.web-security-academy.net\r\n\r\nGET /post?postId=1 HTTP/1.1\r\nFoo: bar
```

(method **HEAD** lets you see the tunnelled response.)

2. Poison the cache for `/` by tunnelling a request whose response is an
   XSS-reflecting redirect: `/resources` (no trailing slash) redirects to
   `/resources/`, reflecting the query — inject the payload in the query
   string:

```
GET /resources?<script>alert(1)</script> HTTP/1.1
```

3. If it times out, the tunnelled response is **shorter** than the main
   response's `Content-Length` — pad the payload with arbitrary characters
   after `</script>` until its length exceeds the noted `Content-Length`.
4. Send until the cache for `/` stores the poisoned response — the victim
   executes it — lab solved.
