# Cross Site Scripting — PortSwigger Web Security Academy


> ⚠️ **Link check 2026-10-17:** 3 lab(s) from the personal tracker have no matching live page on portswigger.net — they may not exist as separate labs. Verify before hunting:

- *"DOM XSS in AngularJS expression with simplified sandbox escape"*
- *"Reflected XSS blocked by CSP with unsafe-eval and script-src restricted to a CDN"*
- *"Stored XSS blocked by CSP, with CSP bypass via an upload"*

| # | Lab | Level | Official |
|---|-----|-------|----------|
| 1 | Reflected XSS into HTML context with nothing encoded | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded) | ✅ [01-reflected-html-context.md](01-reflected-html-context.md) |
| 2 | Stored XSS into HTML context with nothing encoded | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/stored/lab-html-context-nothing-encoded) | ✅ [02-stored-html-context.md](02-stored-html-context.md) |
| 3 | DOM XSS in document.write sink using source location.search | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink) | ✅ [03-dom-document-write.md](03-dom-document-write.md) |
| 4 | DOM XSS in innerHTML sink using source location.search | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-innerhtml-sink) | ✅ [04-dom-innerhtml.md](04-dom-innerhtml.md) |
| 5 | Reflected XSS into HTML context with most tags and attributes blocked | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-most-tags-and-attributes-blocked) | ✅ [05-most-tags-blocked.md](05-most-tags-blocked.md) |
| 6 | Reflected XSS into a JavaScript string with single quote and backslash escaped | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-single-quote-backslash-escaped) | ✅ [06-javascript-string-quotes-escaped.md](06-javascript-string-quotes-escaped.md) |
| 7 | Reflected XSS into a JavaScript string with angle brackets HTML encoded | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-html-encoded) | ✅ [07-javascript-string-angle-brackets-encoded.md](07-javascript-string-angle-brackets-encoded.md) |
| 8 | DOM XSS in document.write sink using source location.search inside a select element | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-document-write-sink-inside-select-element) | ✅ [08-document-write-select.md](08-document-write-select.md) |
| 9 | DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-angularjs-expression) | ✅ [09-angularjs-expression.md](09-angularjs-expression.md) |
| 10 | Reflected XSS into a template literal with angle brackets, single, double quotes, and backslash escaped | — | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-template-literal-angle-brackets-single-double-quotes-backslash-backticks-escaped) | ✅ [10-template-literal.md](10-template-literal.md) |
| 11 | Reflected XSS with some SVG markup allowed | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-some-svg-markup-allowed) | ✅ [14-svg-markup.md](14-svg-markup.md) |
| 12 | Reflected XSS with event handlers and href attributes blocked | EXPERT | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-event-handlers-and-href-attributes-blocked) | ✅ [15-event-handlers-href.md](15-event-handlers-href.md) |
| 13 | Reflected XSS in a canonical link tag | — | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-canonical-link-tag) | ✅ [16-canonical-link-tag.md](16-canonical-link-tag.md) |
| 14 | Exploiting cross-site scripting to steal cookies | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-stealing-cookies) | ✅ [17-stealing-cookies.md](17-stealing-cookies.md) |
| 15 | Exploiting cross-site scripting to capture passwords | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-capturing-passwords) | ✅ [18-capturing-passwords.md](18-capturing-passwords.md) |
| 16 | DOM XSS in jQuery anchor href attribute sink using location.search source | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-href-attribute-sink) | ✅ [19-jquery-href-sink.md](19-jquery-href-sink.md) |
| 17 | DOM XSS in jQuery selector sink using a hashchange event | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-jquery-selector-hash-change-event) | ✅ [20-jquery-selector-hashchange.md](20-jquery-selector-hashchange.md) |
| 18 | Exploiting XSS to bypass CSRF defenses | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/exploiting/lab-perform-csrf) | ✅ [21-bypass-csrf.md](21-bypass-csrf.md) |
| 19 | Reflected DOM XSS | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected) | ✅ [22-reflected-dom-xss.md](22-reflected-dom-xss.md) |
| 20 | Reflected XSS in a JavaScript URL with some characters blocked | EXPERT | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-url-some-characters-blocked) | ✅ [23-javascript-url-blocked-chars.md](23-javascript-url-blocked-chars.md) |
| 21 | Reflected XSS into HTML context with all tags blocked except custom ones | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-html-context-with-all-standard-tags-blocked) | ✅ [24-custom-tags.md](24-custom-tags.md) |
| 22 | Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-javascript-string-angle-brackets-double-quotes-encoded-single-quotes-escaped) | ✅ [25-js-string-single-quotes-escaped.md](25-js-string-single-quotes-escaped.md) |
| 23 | Reflected XSS into attribute with angle brackets HTML-encoded | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-attribute-angle-brackets-html-encoded) | ✅ [26-attribute-angle-brackets-encoded.md](26-attribute-angle-brackets-encoded.md) |
| 24 | Reflected XSS protected by CSP, with CSP bypass | EXPERT | [lab](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-csp-bypass) | ✅ [27-csp-bypass.md](27-csp-bypass.md) |
| 25 | Reflected XSS protected by very strict CSP, with dangling markup attack | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/content-security-policy/lab-very-strict-csp-with-dangling-markup-attack) | ✅ [28-csp-dangling-markup.md](28-csp-dangling-markup.md) |
| 26 | Reflected XSS with AngularJS sandbox escape and CSP | EXPERT | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-and-csp) | ✅ [29-angularjs-sandbox-csp.md](29-angularjs-sandbox-csp.md) |
| 27 | Reflected XSS with AngularJS sandbox escape without strings | EXPERT | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-without-strings) | ✅ [30-angularjs-sandbox-without-strings.md](30-angularjs-sandbox-without-strings.md) |
| 28 | Stored DOM XSS | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-stored) | ✅ [31-stored-dom-xss.md](31-stored-dom-xss.md) |
| 29 | Stored XSS into anchor href attribute with double quotes HTML-encoded | APPRENTICE | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-href-attribute-double-quotes-html-encoded) | ✅ [32-anchor-href-double-quotes.md](32-anchor-href-double-quotes.md) |
| 30 | Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped | PRACTITIONER | [lab](https://portswigger.net/web-security/cross-site-scripting/contexts/lab-onclick-event-angle-brackets-double-quotes-html-encoded-single-quotes-backslash-escaped) | ✅ [33-onclick-event.md](33-onclick-event.md) |
| 31 | Stored XSS blocked by CSP, with CSP bypass via an upload | — | — | — |
| 32 | Reflected XSS protected by very strict CSP, with dangling markup attack | — | — | — |
| 33 | Reflected XSS with AngularJS sandbox escape without strings | — | — | — |

*Solution write-ups: the numbered files in this folder (01-..., 02-...) are the full solutions for each lab.*
