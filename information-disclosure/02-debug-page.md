# Lab 02 — Information disclosure on debug page

> **Apprentice** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-on-debug-page)

**Entry point:** an HTML comment points to a debug page that leaks
environment variables.

## Solution

1. In Burp **Target → Site map**, right-click the lab → *Engagement tools →
   Find comments*: the home page contains a comment linking
   `/cgi-bin/phpinfo.php`.
2. Request `/cgi-bin/phpinfo.php` — the phpinfo output includes the
   `SECRET_KEY` environment variable.
3. Submit the `SECRET_KEY` value — lab solved.

## Mitigation

Remove debug endpoints from production; strip HTML comments in templates.
