# Cross Site Scripting — PortSwigger Web Security Academy


> ⚠️ **Link check 2026-10-17:** 3 lab(s) from the personal tracker have no matching live page on portswigger.net — they may not exist as separate labs. Verify before hunting:

- *"DOM XSS in AngularJS expression with simplified sandbox escape"*
- *"Reflected XSS blocked by CSP with unsafe-eval and script-src restricted to a CDN"*
- *"Stored XSS blocked by CSP, with CSP bypass via an upload"*

| # | Lab | Level | Official |

*Solution write-ups: the numbered files in this folder (`01-...`, `02-...`) are the full solutions for each lab.*
|---|-----|-------|----------|
| 1 | Reflected XSS into HTML context with nothing encoded | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded) |
| 2 | Stored XSS into HTML context with nothing encoded | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded) |
| 3 | DOM XSS in document.write sink using source location.search | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink) |
| 4 | DOM XSS in innerHTML sink using source location.search | Apprentice | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink) |
| 5 | Reflected XSS into HTML context with most tags and attributes blocked | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked) |
| 6 | Reflected XSS into a JavaScript string with single quote and backslash escaped | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped) |
| 7 | Reflected XSS into a JavaScript string with angle brackets HTML encoded | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded) |
| 8 | DOM XSS in document.write sink using source location.search inside a select element | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element) |
| 9 | DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression) |
| 10 | Reflected XSS into a template literal with angle brackets, single, double quotes, and backslash escaped | Expert | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped) |
| 11 | DOM XSS in AngularJS expression with simplified sandbox escape | Expert | — |
| 12 | Reflected XSS blocked by CSP with unsafe-eval and script-src restricted to a CDN | Expert | — |
| 13 | Stored XSS blocked by CSP, with CSP bypass via an upload | Expert | — |
| 14 | Reflected XSS with some SVG markup allowed | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed) |
| 15 | Reflected XSS with event handlers and href attributes blocked | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked) |
| 16 | Reflected XSS in a canonical link tag | Expert | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag) |
| 17 | Exploiting XSS to steal cookies | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-stealing-cookies) |
| 18 | Exploiting XSS to capture passwords | Practitioner | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-capturing-passwords) |
| 19 | Lab: DOM XSS in jQuery anchor href attribute sink using location.search source | Web Security Academy | APPRENTICE | ✅ [19-jquery-href-sink.md](19-jquery-href-sink.md) |
| 20 | Lab: DOM XSS in jQuery selector sink using a hashchange event | Web Security Academy | APPRENTICE | ✅ [20-jquery-selector-hashchange.md](20-jquery-selector-hashchange.md) |
| 21 | Lab: Exploiting XSS to bypass CSRF defenses | Web Security Academy | PRACTITIONER | ✅ [21-bypass-csrf.md](21-bypass-csrf.md) |
| 22 | Lab: Reflected DOM XSS | Web Security Academy | — | ✅ [22-reflected-dom-xss.md](22-reflected-dom-xss.md) |
| 23 | Lab: Reflected XSS in a JavaScript URL with some characters blocked | Web Security Academy | EXPERT | ✅ [23-javascript-url-blocked-chars.md](23-javascript-url-blocked-chars.md) |
| 24 | Lab: Reflected XSS into HTML context with all tags blocked except custom ones | Web Security Academy | PRACTITIONER | ✅ [24-custom-tags.md](24-custom-tags.md) |
| 25 | Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped | Web Security Academy | PRACTITIONER | ✅ [25-js-string-single-quotes-escaped.md](25-js-string-single-quotes-escaped.md) |
| 26 | Lab: Reflected XSS into attribute with angle brackets HTML-encoded | Web Security Academy | APPRENTICE | ✅ [26-attribute-angle-brackets-encoded.md](26-attribute-angle-brackets-encoded.md) |
| 27 | Lab: Reflected XSS protected by CSP, with CSP bypass | Web Security Academy | EXPERT | ✅ [27-csp-bypass.md](27-csp-bypass.md) |
| 28 | Lab: Reflected XSS protected by very strict CSP, with dangling markup attack | Web Security Academy | PRACTITIONER | ✅ [28-csp-dangling-markup.md](28-csp-dangling-markup.md) |
| 29 | Lab: Reflected XSS with AngularJS sandbox escape and CSP | Web Security Academy | EXPERT | ✅ [29-angularjs-sandbox-csp.md](29-angularjs-sandbox-csp.md) |
| 30 | Lab: Reflected XSS with AngularJS sandbox escape without strings | Web Security Academy | EXPERT | ✅ [30-angularjs-sandbox-without-strings.md](30-angularjs-sandbox-without-strings.md) |
| 31 | Lab: Stored DOM XSS | Web Security Academy | — | ✅ [31-stored-dom-xss.md](31-stored-dom-xss.md) |
| 32 | Lab: Stored XSS into anchor href attribute with double quotes HTML-encoded | Web Security Academy | APPRENTICE | ✅ [32-anchor-href-double-quotes.md](32-anchor-href-double-quotes.md) |
| 33 | Lab: Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped | Web Security Academy | PRACTITIONER | ✅ [33-onclick-event.md](33-onclick-event.md) |
