# Lab 05 — SSTI with information disclosure via user-supplied objects

> **Expert** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-with-information-disclosure-via-user-supplied-objects)

**Entry point:** product description template (`content-manager:C0nt3ntM4n4g3r`)
· **Engine:** Django · **Goal:** leak `SECRET_KEY`.

## Solution

1. Detect — save the fuzz string `${{<%[%'"}}%\` as a description; the error
   identifies **Django**.
2. Recon — Django ships a built-in debug tag. Save:

```
{% debug %}
```

The rendered output lists every object in scope — including `settings`.

3. Exploit — replace the debug tag with:

```
{{settings.SECRET_KEY}}
```

4. Save and view the product page: the rendered `SECRET_KEY` value is the
   solution — submit it — lab solved.

## Notes

`{% debug %}` is the fastest recon primitive in Django SSTI: it maps the
whole context for you.
