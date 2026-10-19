# Lab 02 — Information disclosure on debug page

> **Apprentice** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-on-debug-page)

**Entry point:** an HTML comment points to a debug page that leaks

> **Burp Community alternative (free):** the tool named below is Pro-only — the free replacement is described in the steps.
environment variables.

## Solution

1. View the home page **source** (Ctrl+U — Community tip: no engagement
   tools needed, comments are visible in the source): it contains a comment
   linking `/cgi-bin/phpinfo.php`.
2. Request `/cgi-bin/phpinfo.php` — the phpinfo output includes the
   `SECRET_KEY` environment variable.
3. Submit the `SECRET_KEY` value — lab solved.

## Mitigation

Remove debug endpoints from production; strip HTML comments in templates.
