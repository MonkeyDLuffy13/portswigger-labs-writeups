# Lab 05 — Web cache deception (tracker entry)

> Tracker entry · the original lab page is no longer live on the Academy —
> the live related lab is [Internal cache poisoning](https://portswigger.net/web-security/web-cache-poisoning/exploiting-implementation-flaws/lab-web-cache-poisoning-internal).

## The technique (for real-world targets)

Web cache deception tricks a **victim** into requesting a URL that (a)
returns their private data and (b) looks cacheable to the cache — so the
response, containing the victim's data, is stored and served to you.

1. Find a path suffix the cache treats as static: `/my-account/foo.css`,
   `/my-account/foo.js`, `/settings;.js`, `/profile%0d%0a.js`...
2. Build a page that makes the logged-in victim load that URL:

```html
<img src="https://TARGET/my-account/deception.css">
```

3. Deliver to the victim. The cache stores their account page under the
   `.css` key.
4. Request the same URL yourself — the cached response contains the
   victim's private data.

## Variants

- Path-parameter delimiters (`;`, `:`) on various caches/frameworks.
- Encoding tricks (`%0d%0a`, double slashes).
- Cache-rule abuse of extensions (`.js`, `.css`, `.ico`).

## Mitigation

Don't let static-resource cache rules apply to authenticated, dynamic
endpoints; mark private responses `Cache-Control: private, no-store`.
