# Lab 14 — User ID controlled by request parameter, with unpredictable user IDs

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter-with-unpredictable-user-ids)

**Entry point:** user ids are GUIDs — but leaked in blog post bylines.

## Solution

1. Find a blog post authored by carlos; click the author link — the URL
   contains his GUID (`/blogs?userId=...`). Save it.
2. Log in, change `GET /my-account?id=<carlos-guid>`.
3. His API key renders — submit it — lab solved.

## Mitigation

Unpredictable ids slow enumeration but leak anywhere (bylines, logs,
emails) they become IDOR keys — authorize per request.
