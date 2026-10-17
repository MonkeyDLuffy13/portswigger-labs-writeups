# Lab 01 — Basic server-side template injection

> **Apprentice** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic)

**Entry point:** `GET /?message=` on the out-of-stock page · **Engine:** Ruby ERB.

## Solution

1. Detect — the `message` parameter is rendered through a template:

```
<%= 7*7 %>
```

→ the page shows **49**: code evaluation confirmed (SSTI).

2. Exploit — ERB tags execute Ruby; `system()` runs shell commands:

```
<%= system("rm /home/carlos/morale.txt") %>
```

URL-encoded in `message` — the file is deleted — lab solved.

## Methodology (applies to every SSTI lab)

1. Probe with a math payload in each engine's syntax (`${7*7}`, `<%= 7*7 %>`,
   `{{7*7}}`, `#{7*7}`).
2. Identify the engine from which syntax works / the error message.
3. Read that engine's documentation for code execution, then exploit.
