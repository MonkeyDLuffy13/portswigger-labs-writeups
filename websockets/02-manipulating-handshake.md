# Lab 02 — Manipulating the WebSocket handshake to exploit vulnerabilities

> **Expert** · [Official lab](https://portswigger.net/web-security/websockets/lab-manipulating-handshake-to-exploit-vulnerabilities)

**Entry point:** the WS handshake is editable in Repeater — the filter bans
your IP and blocks known payloads.

## Solution

1. Open Live chat, send a message, send the message request to
   **Repeater** (WS mode) and try `<img src=1 onerror='alert(1)'>` — blocked,
   and the connection drops.
2. Reconnect fails: **your IP is banned**. Spoof it on the *handshake*
   request by adding:

```http
X-Forwarded-For: 1.1.1.1
```

3. Connect, then send the payload obfuscated to evade the blacklist —
   mixed-case handler + backticks instead of quotes:

```json
{"message":"<img src=1 oNeRrOr=alert`1`>"}
```

4. The support agent renders it and the alert fires in **their** browser —
   lab solved.

## Notes

Three stacked lessons: trust headers (`X-Forwarded-For` is client-controlled),
blacklists fail on case/backticks, and WS handshakes are ordinary HTTP.
