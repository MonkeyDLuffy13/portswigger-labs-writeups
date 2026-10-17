# Lab 03 — Exploiting Java deserialization with Apache Commons

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-exploiting-java-deserialization-with-apache-commons)

**Entry point:** the session cookie is a URL+Base64-encoded **serialized Java
object**; the app ships Apache Commons Collections.

## Solution

1. Log in (`wiener:peter`) and confirm the serialized-Java session cookie.
2. Generate a gadget payload with **ysoserial** (`CommonsCollections4` runs
   the command via `Runtime`):

```bash
java -jar ysoserial-all.jar CommonsCollections4 'rm /home/carlos/morale.txt' | base64
```

(Java 16+: add the `--add-opens` flags ysoserial prints for
`java.xml`/`java.base` packages.)

3. Replace the session cookie with the generated payload and **URL-encode**
   the whole value.
4. Send any in-scope request — deserialization executes the command —
   lab solved.

## Mitigation

Never deserialize untrusted Java streams; prefer JSON with schema
validation. If unavoidable, filter incoming classes
(`ObjectInputFilter`) and keep Commons Collections patched.
