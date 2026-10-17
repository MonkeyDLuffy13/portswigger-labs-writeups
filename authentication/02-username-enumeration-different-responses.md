# Lab 02 — Username enumeration via different responses

> **Apprentice** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-different-responses)

**Entry point:** `POST /login` — distinct error messages per failure type.

## Solution

1. `wiener:peter` → valid login; wrong password for wiener →
   `"Incorrect password"`; unknown user → `"Invalid username"` — the
   difference enumerates users.
2. Burp Intruder, sniper on `username` (candidate list), fixed password:
   any response saying **"Incorrect password"** = valid username →
   `armando`? no — in this lab the valid username is `alice`... run the list
   and take the one that differs.
3. Second attack: fix the valid username, sniper on `password` — the
   response that shows **"Incorrect password"**-style success redirect
   (302) is the valid password.
4. Log in as the victim — lab solved.

## Mitigation

One identical generic message for every login failure, same status code,
same timing.
