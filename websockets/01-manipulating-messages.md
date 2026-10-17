# Lab 01 — Manipulating WebSocket messages to exploit vulnerabilities

> **Practitioner** · [Official lab](https://portswigger.net/web-security/websockets/lab-manipulating-messages-to-exploit-vulnerabilities)

**Entry point:** live-chat WebSocket messages — rendered by the support
agent without encoding, with a naive input filter.

## Solution

1. Open Live chat, send a message; in **Proxy → WebSockets history** you see
   `{"message":"hello"}`. Send it to Repeater.
2. Send an XSS probe — the filter blocks obvious payloads
   (`<script>` is blacklisted, repeated offenses terminate the connection).
3. Bypass the naive filter with an event handler instead:

```json
{"message":"<img src=1 onerror=alert(1)>"}
```

The support agent's browser renders it — lab solved.

## Mitigation

Encode chat content on render (or sanitize server-side); never rely on a
client-controlled blacklist.
