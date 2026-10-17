# Lab 07 — Broken brute-force protection, IP block

> **Practitioner** · [Official lab](https://portswigger.net/web-security/authentication/password-based/lab-broken-bruteforce-protection-ip-block)

**Entry point:** your IP is blocked after 2 wrong passwords — but the
counter resets on a **valid** login for *any* user.

## Solution

1. Craft a candidate list that alternates: your own valid password
   (`peter`) after every 2 guesses at carlos's password:

```
pass1, pass2, peter, pass3, pass4, peter, ...
```

2. Intruder (sniper on `password`, username fixed `carlos`) — every third
   request is your valid login, resetting the IP block.
3. One attempt returns **302** — that's carlos's password — log in —
   lab solved.

## Notes

IP blocks that reset on any successful login are bypassable by
interleaving your own account's logins.
