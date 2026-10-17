# Lab 02 — Blind OS command injection with time delays

> **Practitioner** · [Official lab](https://portswigger.net/web-security/os-command-injection/lab-blind-time-delays)

**Entry point:** `POST /feedback` — the "Website" field is passed to a shell,
but output is never returned.

## Solution

1. Submit feedback normally and note the request fields (`name`, `email`,
   `subject`, `message`, `website`...).
2. Probe each field with a ping — the `email` field is the vulnerable one:

```
email=x||ping+-c+10+127.0.0.1||
```

3. The response takes **~10 seconds** — blind command injection confirmed —
   lab solved.

## Notes

`||` runs the ping when the left side fails (the email value is not a
command). Time-based exfiltration is the only channel when output is
discarded.
