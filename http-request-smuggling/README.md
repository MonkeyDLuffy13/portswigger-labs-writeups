# Http Request Smuggling — PortSwigger Web Security Academy


> ⚠️ **Link check 2026-10-17:** 2 lab(s) from the personal tracker have no matching live page on portswigger.net — they may not exist as separate labs. Verify before hunting:

- *"H2.TE vulnerability"*
- *"TE.H2 vulnerability"*

| # | Lab | Level | Official |
|---|-----|-------|----------|
| 1 | HTTP request smuggling, basic CL.TE vulnerability | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/lab-basic-cl-te) | ✅ [01-cl-te.md](01-cl-te.md) |
| 2 | HTTP request smuggling, basic TE.CL vulnerability | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/lab-basic-te-cl) | ✅ [02-te-cl.md](02-te-cl.md) |
| 3 | 0.CL request smuggling | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/browser/cl-0/lab-cl-0-request-smuggling) | ✅ [05-0cl.md](05-0cl.md) |
| 4 | CL.0 request smuggling | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/browser/cl-0/lab-cl-0-request-smuggling) | ✅ [06-cl-0.md](06-cl-0.md) |
| 5 | Client-side desync | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/browser/client-side-desync) | ✅ [07-client-side-desync.md](07-client-side-desync.md) |
| 6 | Exploiting HTTP request smuggling to bypass front-end security controls (CL.TE) | — | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-cl-te) | ✅ [08-bypass-frontend-cl-te.md](08-bypass-frontend-cl-te.md) |
| 7 | Exploiting HTTP request smuggling to bypass front-end security controls (TE.CL) | — | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-cl-te) | ✅ [09-bypass-frontend-te-cl.md](09-bypass-frontend-te-cl.md) |
| 8 | Exploiting HTTP request smuggling to reveal front-end request rewriting | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-reveal-front-end-request-rewriting) | ✅ [10-reveal-rewriting.md](10-reveal-rewriting.md) |
| 9 | Exploiting HTTP request smuggling to capture other users' requests | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-capture-other-users-requests) | ✅ [11-capture-users-requests.md](11-capture-users-requests.md) |
| 10 | Exploiting HTTP request smuggling to deliver reflected XSS | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-deliver-reflected-xss) | ✅ [12-deliver-reflected-xss.md](12-deliver-reflected-xss.md) |
| 11 | Exploiting HTTP request smuggling to perform web cache poisoning | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-poisoning) | ✅ [13-web-cache-poisoning.md](13-web-cache-poisoning.md) |
| 12 | Exploiting HTTP request smuggling to perform web cache deception | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-deception) | ✅ [14-web-cache-deception.md](14-web-cache-deception.md) |
| 13 | HTTP request smuggling, confirming a CL.TE vulnerability via differential responses | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-cl-te-via-differential-responses) | ✅ [15-confirm-cl-te.md](15-confirm-cl-te.md) |
| 14 | HTTP request smuggling, confirming a TE.CL vulnerability via differential responses | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-cl-te-via-differential-responses) | ✅ [16-confirm-te-cl.md](16-confirm-te-cl.md) |
| 15 | HTTP request smuggling, obfuscating the TE header | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/lab-obfuscating-te-header) | ✅ [17-obfuscating-te-header.md](17-obfuscating-te-header.md) |
| 16 | H2.CL request smuggling | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-cl-request-smuggling) | ✅ [18-h2-cl.md](18-h2-cl.md) |
| 17 | HTTP/2 request smuggling via CRLF injection | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-smuggling-via-crlf-injection) | ✅ [19-h2-crlf-injection.md](19-h2-crlf-injection.md) |
| 18 | HTTP/2 request splitting via CRLF injection | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection) | ✅ [20-h2-request-splitting.md](20-h2-request-splitting.md) |
| 19 | Response queue poisoning via H2.TE request smuggling | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/response-queue-poisoning/lab-request-smuggling-h2-response-queue-poisoning-via-te-request-smuggling) | ✅ [21-h2-te-queue-poisoning.md](21-h2-te-queue-poisoning.md) |
| 20 | Server-side pause-based request smuggling | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/browser/pause-based-desync/lab-server-side-pause-based-request-smuggling) | ✅ [22-pause-based-smuggling.md](22-pause-based-smuggling.md) |
| 21 | Web cache poisoning via HTTP/2 request tunnelling | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-web-cache-poisoning-via-request-tunnelling) | ✅ [23-h2-tunnelling-cache-poisoning.md](23-h2-tunnelling-cache-poisoning.md) |
| 22 | Bypassing access controls via HTTP/2 request tunnelling | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-bypass-access-controls-via-request-tunnelling) | ✅ [24-h2-tunnelling-bypass-access-controls.md](24-h2-tunnelling-bypass-access-controls.md) |
| 23 | H2.TE vulnerability | — | — | — |
| 24 | TE.H2 vulnerability | — | — | — |

*Solution write-ups: the numbered files in this folder (01-..., 02-...) are the full solutions for each lab.*
