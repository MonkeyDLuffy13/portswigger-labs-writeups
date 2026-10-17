# Lab 04 — Web cache poisoning: cache key injection via URL path

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-cache-key-injection)

**Entry point:** `/login?lang=en` — `utm_content` is excluded from the cache
key after `lang`, enabling key injection into the cached redirect.

## Solution

1. **Unkeyed param:** `/login?lang=en?utm_content=x` — the `?` inside the
   value leaves `utm_content` unkeyed, so arbitrary content rides along.
2. **Pollution vector:** `/login/` imports `/js/localize.js`, which does not
   URL-encode the `lang` value (client-side parameter pollution).
3. **Header injection:** adding `cors=1` makes the endpoint reflect the
   `Origin` header — including CRLF.
4. Confirm with `Pragma: x-get-cache-key` that cache-key injection works.
5. Poison with the crafted path (HTTP/2 — injected headers must be
   lowercase), all injected through the URL:

```http
GET /login?lang=en?utm_content=x%26cors=1%26x=1$$origin=x%250d%250aContent-Length:%208%250d%250a%250d%250aalert(1)$$%23 HTTP/2
```

6. The cache for `/login?lang=en` now serves a poisoned redirect whose
   localize import is also poisoned — the victim's browser executes
   `alert(1)` — lab solved.

## Notes

`$$...$$` delimits the injected response body; `%250d%250a` is the
double-encoded CRLF that splits the poisoned JavaScript response.
