# Lab 24 — Bypassing access controls via HTTP/2 request tunnelling

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-bypass-access-controls-via-request-tunnelling)

**Entry point:** the front-end appends client-auth headers
(e.g. `X-SSL-CLIENT-CN: administrator`) — tunnel a request long enough to
reflect them.

## Solution

1. Tunnel a request to an endpoint that reflects request content (search
   function), using the `:path` technique with an oversized
   `Content-Length` in the tunnelled request:

```
:path: /?cachebuster=1 HTTP/1.1\r\nHost: LAB\r\n\r\nPOST /search HTTP/1.1\r\nHost: LAB\r\nContent-Length: 500\r\n\r\nq=
```

(The appended auth headers land inside the tunnelled body → reflected.)

2. Note the exact auth header, e.g. `X-SSL-CLIENT-CN: administrator`.
3. Tunnel a request to `/admin` carrying that header yourself, then
   `/admin/delete?username=carlos` — lab solved.

## Notes

Tunnelling turns front-end-injected security headers into readable (and
forgeable) content — never trust appended headers for authorization.
