# Lab 20 — HTTP/2 request smuggling via CRLF injection

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/advanced/lab-request-smuggling-h2-request-smuggling-via-crlf-injection)

**Entry point:** HTTP/2 headers may contain `\r\n` — the downgrade writes
them raw into the HTTP/1.1 request.

## Solution

1. In Repeater (HTTP/2), drill into a header in the Inspector and press
   **Shift+Return** to insert a newline (double-click won't allow it).
2. Inject a smuggled request through the header — e.g. `foo` header with
   value ending in a full second request, or a `content-length: 0`-style
   split via the `:path`/headers.
3. The downgraded HTTP/1.1 request now contains your injected framing —
   the next request on the connection receives your smuggled response —
   lab solved.

## Notes

HTTP/2 forbids CR/LF in header values, but front-ends that rebuild HTTP/1.1
without re-validating them reintroduce the classic desync.
