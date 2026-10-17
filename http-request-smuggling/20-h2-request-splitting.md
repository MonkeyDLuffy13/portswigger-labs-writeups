# Lab 21 — HTTP/2 request splitting via CRLF injection

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-splitting-via-crlf-injection)

**Entry point:** same CRLF injection, used to **split** one HTTP/2 request
into two HTTP/1.1 requests instead of smuggling a prefix.

## Solution

1. Repeater (HTTP/2) → Inspector → add a CRLF via **Shift+Return** inside a
   header value to close the first request and start a second one.
2. Craft two complete requests in one, e.g. through `:path`/header values,
   so the downgrade emits both.
3. Verify by receiving responses for both requests (the second can target
   any path the front-end would normally block) — lab solved.

## Notes

Splitting vs smuggling is framing granularity: both stem from trusting
attacker-controlled header bytes during HTTP/2 → HTTP/1.1 translation.
