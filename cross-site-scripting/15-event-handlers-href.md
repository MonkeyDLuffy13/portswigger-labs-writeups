# Lab 15 — Reflected XSS with event handlers and href attributes blocked

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/event-handlers-href)

**Entry point:** `GET /?search=` · **Obstacle:** all event handlers and plain
`href` are blocked — but `xlink:href` inside SVG is not.

## Solution

1. Probe: tags are allowed; `on*` and `href=` are stripped. SVG namespaced
   attributes (`xlink:href`) bypass the filter.
2. Build a clickable SVG link that executes `javascript:`:

```html
<svg><a xlink:href="javascript:alert(1)"><text x=20 y=20>Click me</text></a></svg>
```

3. Inject via `?search=` and **click the "Click me" text** in the injected
   area — lab solves on execution.

## Notes

The WAF regex checks for `href` but misses `xlink:href`. Always test
namespaced attributes when allow-lists look impenetrable.
