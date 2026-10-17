# Http Request Smuggling — PortSwigger Web Security Academy

> Tracker name (Arabic): **تهريب طلبات HTTP** · 4 labs · ✅ solved — all 22 labs

> ⚠️ **Link check 2026-10-17:** 2 lab(s) from the personal tracker have no matching live page on portswigger.net — they may not exist as separate labs. Verify before hunting:

- *"H2.TE vulnerability"*
- *"TE.H2 vulnerability"*

| # | Lab | Level | Official | Solution |
|---|-----|-------|----------|----------|
| 1 | CL.TE vulnerability | Practitioner | [lab](https://portswigger.net/web-security/request-smuggling/lab-basic-cl-te) | ✅ [01-cl-te.md](01-cl-te.md) |
| 2 | TE.CL vulnerability | Practitioner | [lab](https://portswigger.net/web-security/request-smuggling/lab-basic-te-cl) | ✅ [02-te-cl.md](02-te-cl.md) |
| 3 | H2.TE vulnerability | Expert | — | — |
| 4 | TE.H2 vulnerability | Expert | — | — |
| 5 | Lab: 0.CL request smuggling | Web Security Academy | — | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-0cl-request-smuggling) | ✅ [05-0cl.md](05-0cl.md) |
| 6 | Lab: Bypassing access controls via HTTP/2 request tunnelling | Web Security Academy | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-bypass-access-controls-via-request-tunnelling) | ✅ [06-cl-0.md](06-cl-0.md) |
| 7 | Lab: CL.0 request smuggling | Web Security Academy | — | [lab](https://portswigger.net/web-security/request-smuggling/browser/cl-0/lab-cl-0-request-smuggling) | ✅ [07-client-side-desync.md](07-client-side-desync.md) |
| 8 | Lab: Client-side desync | Web Security Academy | — | [lab](https://portswigger.net/web-security/request-smuggling/browser/client-side-desync/lab-client-side-desync) | ✅ [08-bypass-frontend-cl-te.md](08-bypass-frontend-cl-te.md) |
| 9 | Lab: Exploiting HTTP request smuggling to bypass front-end security controls, CL.TE vulnerability | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-cl-te) | ✅ [09-bypass-frontend-te-cl.md](09-bypass-frontend-te-cl.md) |
| 10 | Lab: Exploiting HTTP request smuggling to bypass front-end security controls, TE.CL vulnerability | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-bypass-front-end-controls-te-cl) | ✅ [10-reveal-rewriting.md](10-reveal-rewriting.md) |
| 11 | Lab: Exploiting HTTP request smuggling to capture other users&#x27; requests | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-capture-other-users-requests) | ✅ [11-capture-users-requests.md](11-capture-users-requests.md) |
| 12 | Lab: Exploiting HTTP request smuggling to deliver reflected XSS | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-deliver-reflected-xss) | ✅ [12-deliver-reflected-xss.md](12-deliver-reflected-xss.md) |
| 13 | Lab: Exploiting HTTP request smuggling to perform web cache deception | Web Security Academy | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-deception) | ✅ [13-web-cache-poisoning.md](13-web-cache-poisoning.md) |
| 14 | Lab: Exploiting HTTP request smuggling to perform web cache poisoning | Web Security Academy | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-perform-web-cache-poisoning) | ✅ [14-web-cache-deception.md](14-web-cache-deception.md) |
| 15 | Lab: Exploiting HTTP request smuggling to reveal front-end request rewriting | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/exploiting/lab-reveal-front-end-request-rewriting) | ✅ [15-confirm-cl-te.md](15-confirm-cl-te.md) |
| 16 | Lab: H2.CL request smuggling | Web Security Academy | — | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-cl-request-smuggling) | ✅ [16-confirm-te-cl.md](16-confirm-te-cl.md) |
| 17 | Lab: HTTP request smuggling, confirming a CL.TE vulnerability via differential responses | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-cl-te-via-differential-responses) | ✅ [17-obfuscating-te-header.md](17-obfuscating-te-header.md) |
| 18 | Lab: HTTP request smuggling, confirming a TE.CL vulnerability via differential responses | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/finding/lab-confirming-te-cl-via-differential-responses) | ✅ [18-h2-cl.md](18-h2-cl.md) |
| 19 | Lab: HTTP request smuggling, obfuscating the TE header | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/lab-obfuscating-te-header) | ✅ [19-h2-crlf-injection.md](19-h2-crlf-injection.md) |
| 20 | Lab: HTTP/2 request smuggling via CRLF injection | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-smuggling-via-crlf-injection) | ✅ [20-h2-request-splitting.md](20-h2-request-splitting.md) |
| 21 | Lab: HTTP/2 request splitting via CRLF injection | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection) | ✅ [21-h2-te-queue-poisoning.md](21-h2-te-queue-poisoning.md) |
| 22 | Lab: Response queue poisoning via H2.TE request smuggling | Web Security Academy | PRACTITIONER | [lab](https://portswigger.net/web-security/request-smuggling/advanced/response-queue-poisoning/lab-request-smuggling-h2-response-queue-poisoning-via-te-request-smuggling) | ✅ [22-pause-based-smuggling.md](22-pause-based-smuggling.md) |
| 23 | Lab: Server-side pause-based request smuggling | Web Security Academy | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/browser/pause-based-desync/lab-server-side-pause-based-request-smuggling) | ✅ [23-h2-tunnelling-cache-poisoning.md](23-h2-tunnelling-cache-poisoning.md) |
| 24 | Lab: Web cache poisoning via HTTP/2 request tunnelling | Web Security Academy | EXPERT | [lab](https://portswigger.net/web-security/request-smuggling/advanced/request-tunnelling/lab-request-smuggling-h2-web-cache-poisoning-via-request-tunnelling) | ✅ [24-h2-tunnelling-bypass-access-controls.md](24-h2-tunnelling-bypass-access-controls.md) |
