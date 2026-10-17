# Lab 22 — Reflected DOM XSS

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/dom-based/lab-dom-xss-reflected)

**Entry point:** search results are returned as JSON and passed to
`eval()`; quotes are escaped but **backslashes are not**.

## Solution

1. Search term reflects inside
   `{"searchTerm":"...", "results":[...]}` → `eval`'d.
2. Inject a backslash to cancel the escaper, then close out:

```
\"-alert(1)}//
```

The JSON becomes `{"searchTerm":"\\"-alert(1)}//",...` — the double
backslash nullifies the escape, `"` closes the string, `-alert(1)` runs,
and `}//` terminates the object — lab solved.
