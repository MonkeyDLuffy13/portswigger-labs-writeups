# Lab 14 — Username enumeration via account lock

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-username-enumeration-via-account-lock)

**Entry point:** 5 failed attempts lock the account — the lock message
differs for valid usernames.

## Solution

1. Intruder **Cluster bomb**: `username` = candidate list, second position =
   **5 null payloads** (each username tried 5×).
2. The valid username's responses are longer — they say *"You have made too
   many incorrect login attempts"* (locks only exist for real accounts).
3. New attack (sniper): that username × password list, **grep-extract** the
   error message — the one response with **no error message** used the
   correct password.
4. Wait 1 minute for the lock to clear, log in — lab solved.

## Notes

Lock messages are enumeration oracles; keep responses uniform and make
locks silent.
