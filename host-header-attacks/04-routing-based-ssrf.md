# Lab 04 — Routing-based SSRF

> **Practitioner** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/lab-host-header-routing-based-ssrf)

**Entry point:** the middleware **routes requests based on the Host

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) (DNS + HTTP). Substitute its domain wherever this write-up says Collaborator/Collaborator payload.
header** — make it route to an internal admin server.

## Solution

1. Confirm: `Host: <Collaborator>` → the middleware issues requests to your
   Collaborator (Poll now).
2. Intruder-scan the internal range: unset "Update Host header to match
   target", set `Host: 192.168.0.§0§` (numbers 0–255).
3. One response is **302 → /admin** — that's the admin back-end. Request
   `GET /admin` with that Host.
4. The delete form needs CSRF + session: craft

```http
GET /admin/delete?csrf=<TOKEN-FROM-PAGE>&username=carlos HTTP/1.1
Host: 192.168.0.x:8080
Cookie: <session from the admin response>
```

(convert to POST as the form does) — carlos deleted — lab solved.

## Notes

Routing-based SSRF: the Host *is* the destination — internal services
trusting the middleware become reachable.
