# Lab 14 — Reflected XSS with some SVG markup allowed

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/svg-markup)

**Entry point:** `GET /?search=` · **Obstacle:** `<script>` and common
handlers are blocked, but some SVG tags pass the WAF.

## Solution

1. Fuzz the allow-list: `<svg>` is allowed but `onload` is stripped; event
   attributes on child SVG elements pass.
2. Use `<animatetransform>` — an SVG animation element — with `onbegin`:

```
<svg><animatetransform onbegin=alert(1) attributeName=transform>
```

3. The animation starts immediately on render, firing `onbegin` — lab solved.

## Notes

`onbegin` fires when the animation element begins — no user interaction
needed. `<animate>` variants work the same way.
