# Cross Site Scripting — PortSwigger Web Security Academy

> Tracker name (Arabic): **هجمات XSS** · 18 labs · ✅ solved — all 6 verified labs
> Link-checked: 2026-10-17 — every resolved URL was verified live (HTTP 200 + matching page title).

> ⚠️ **Link check 2026-10-17:** 3 lab(s) from the personal tracker have no matching live page on portswigger.net — they may not exist as separate labs. Verify before hunting:

- *"DOM XSS in AngularJS expression with simplified sandbox escape"*
- *"Reflected XSS blocked by CSP with unsafe-eval and script-src restricted to a CDN"*
- *"Stored XSS blocked by CSP, with CSP bypass via an upload"*

| # | Lab | Level | Official | Solution |
|---|-----|-------|----------|----------|
| 1 | Reflected XSS into HTML context with nothing encoded | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded) | ✅ [01-reflected-html-context.md](01-reflected-html-context.md) |
| 2 | Stored XSS into HTML context with nothing encoded | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded) | ✅ [02-stored-html-context.md](02-stored-html-context.md) |
| 3 | DOM XSS in document.write sink using source location.search | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink) | ✅ [03-dom-document-write.md](03-dom-document-write.md) |
| 4 | DOM XSS in innerHTML sink using source location.search | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink) | ✅ [04-dom-innerhtml.md](04-dom-innerhtml.md) |
| 5 | Reflected XSS into HTML context with most tags and attributes blocked | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked) | ✅ [05-most-tags-blocked.md](05-most-tags-blocked.md) |
| 6 | Reflected XSS into a JavaScript string with single quote and backslash escaped | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped) | ✅ [06-javascript-string-quotes-escaped.md](06-javascript-string-quotes-escaped.md) |
| 7 | Reflected XSS into a JavaScript string with angle brackets HTML encoded | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded) | ✅ [07-javascript-string-angle-brackets-encoded.md](07-javascript-string-angle-brackets-encoded.md) |
| 8 | DOM XSS in document.write sink using source location.search inside a select element | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element) | ✅ [08-document-write-select.md](08-document-write-select.md) |
| 9 | DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression) | ✅ [09-angularjs-expression.md](09-angularjs-expression.md) |
| 10 | Reflected XSS into a template literal with angle brackets, single, double quotes, and backslash escaped | Expert | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped) | ✅ [10-template-literal.md](10-template-literal.md) |
| 11 | DOM XSS in AngularJS expression with simplified sandbox escape | Expert | — | — |
| 12 | Reflected XSS blocked by CSP with unsafe-eval and script-src restricted to a CDN | Expert | — | — |
| 13 | Stored XSS blocked by CSP, with CSP bypass via an upload | Expert | — | — |
| 14 | Reflected XSS with some SVG markup allowed | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed) | ✅ [14-svg-markup.md](14-svg-markup.md) |
| 15 | Reflected XSS with event handlers and href attributes blocked | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked) | ✅ [15-event-handlers-href.md](15-event-handlers-href.md) |
| 16 | Reflected XSS in a canonical link tag | Expert | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag) | ✅ [16-canonical-link-tag.md](16-canonical-link-tag.md) |
| 17 | Exploiting XSS to steal cookies | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-stealing-cookies) | ✅ [17-stealing-cookies.md](17-stealing-cookies.md) |
| 18 | Exploiting XSS to capture passwords | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-capturing-passwords) | ✅ [18-capturing-passwords.md](18-capturing-passwords.md) |
