# Lab 08 — Developing a custom gadget chain for Java deserialization

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-developing-a-custom-gadget-chain-for-java-deserialization)

**Entry point:** serialized-Java session cookie · the source leaks via
`/backup/*.java` · **Goal:** SQLi through a `readObject()` gadget.

## Solution

1. Find `/backup/AccessTokenUser.java` in the site map; browse `/backup` —
   `ProductTemplate.java` is exposed too.
2. The gadget: `data.productcatalog.ProductTemplate.readObject()` passes the
   object's `id` attribute straight into a SQL statement.
3. Use PortSwigger's **serialization-examples** project (GitHub): edit
   `Main.java` to instantiate `ProductTemplate` with `id = YOUR-PAYLOAD`,
   serialize, Base64 → session cookie. (Hackvertor's template avoids
   recompiling per payload — replace both `YOUR-PAYLOAD-HERE` markers.)
4. Confirm SQLi: `id` = `'` → Postgres error.
5. Error-based UNION (8 columns; columns 4–6 accept non-string types and
   reflect your input in the error):

```
' UNION SELECT NULL, NULL, NULL, CAST(password AS numeric), NULL, NULL, NULL, NULL FROM users--
```

6. The exception leaks the administrator password. Log in as
   `administrator`, delete `carlos` — lab solved.

## Notes

When no public gadget chain exists, read the app's own classes: any
`readObject`/setter that touches files, SQL, or commands is your sink.
