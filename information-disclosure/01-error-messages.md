# Lab 01 — Information disclosure in error messages

> **Apprentice** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-error-messages)

**Entry point:** `GET /product?productId=` — unexpected input triggers a
verbose stack trace.

## Solution

1. Send `GET /product?productId=1` to Repeater.
2. Change the parameter to a non-integer (a string):

```
GET /product?productId="example"
```

3. The 500 response contains a full stack trace revealing the framework and
   its version — **Apache Struts 2 2.3.31**.
4. Submit `2 2.3.31` — lab solved.

## Mitigation

Return generic error pages; log stack traces server-side only.
