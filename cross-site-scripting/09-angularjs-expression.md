# Lab 09 — DOM XSS in AngularJS expression with angle brackets and double quotes HTML-encoded

> **Practitioner** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/angularjs-expression)

**Entry point:** `GET /?search=` — the term lands inside an `ng-app` region,
so AngularJS evaluates it as an expression even though `<`/`"` are encoded.

## Solution

1. Curly braces survive encoding — everything happens inside `{{ }}`.
2. Reach the `Function` constructor through `constructor` and call `alert`:

```
{{constructor.constructor('alert(1)')()}}
```

3. Search with that payload — AngularJS evaluates the expression — lab solved.

## Mitigation

Don't mix user input with client-side templating; upgrade AngularJS (recent
1.x versions sand-box… deprecate expressions entirely) or disable `ng-app`
on user-content regions.
