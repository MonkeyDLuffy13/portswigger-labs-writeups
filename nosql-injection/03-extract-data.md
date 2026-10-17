# Lab 03 — Exploiting NoSQL injection to extract data

> **Practitioner** · [Official lab](https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-extract-data)

**Entry point:** `POST /login` (JSON) — blind, boolean-based password
extraction via `$regex`. Password is lowercase only.

## Solution

1. Log in as wiener; note the JSON login.
2. Use operator injection to keep the username fixed at administrator and
   regex-test the password character by character:

```json
{"username":{"$regex":"admin.*"},
 "password":{"$regex":"^a.*"}}
```

Login succeeds (no *"Invalid username or password"*) only while the regex
matches the real password prefix.

3. In Intruder: position = the character after `^` in the regex; payloads =
   `a-z`; mark valid logins. Extend: `^a.*`, `^bu.*`...
4. Rebuild the full password (e.g. `administrator`... run until no candidate
   matches), then log in as `administrator` — lab solved.

## Notes

Anchor with `^` and grow the known prefix one character at a time —
standard blind `$regex` extraction.
