# Lab 11 — Password brute-force via password change

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/other-mechanisms/lab-password-brute-force-via-password-change)

**Entry point:** `POST /my-account/change-password` — different error
messages for wrong current password vs mismatched new passwords leak the
answer.

## Solution

1. Behavior matrix: correct current + mismatched new →
   *"New passwords do not match"*; wrong current + mismatched new →
   *"Current password is incorrect"*.
2. Intruder on `POST /my-account/change-password`:

```
username=carlos&current-password=§candidate§&new-password-1=123&new-password-2=abc
```

3. Grep-match **"New passwords do not match"** — the one response with that
   message used the correct current password.
4. Log in as `carlos` with it — lab solved.

## Mitigation

Uniform failure messages on password change; rate-limit per account.
