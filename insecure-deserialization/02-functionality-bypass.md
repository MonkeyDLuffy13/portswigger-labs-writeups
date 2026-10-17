# Lab 02 — Using application functionality to exploit insecure deserialization

> **Practitioner** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-using-application-functionality-to-exploit-insecure-deserialization)

**Entry point:** the delete-account feature reads the serialized
`avatar_link` path and deletes that file — an arbitrary file-deletion
primitive.

## Solution

1. Log in (`wiener:peter`); note **Delete account** (`POST /my-account/delete`).
2. Inspect the session cookie: the object contains

```
s:11:"avatar_link";s:19:"/home/wiener/avatar.png";
```

3. Redirect the link at the target file (adjust the length indicators —
   `23` = strlen of `/home/carlos/morale.txt`):

```
s:11:"avatar_link";s:23:"/home/carlos/morale.txt";
```

4. Re-encode the cookie and send `POST /my-account/delete` — the handler
   deletes the file at `avatar_link` — lab solved.

## Notes

No gadget chain needed: application features consuming deserialized values
are themselves the exploit primitive.
