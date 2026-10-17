# Lab 08 — DOM-based open redirection

> **Apprentice** · [Official lab](https://portswigger.net/web-security/dom-based/open-redirection/lab-dom-open-redirection)

**Entry point:** the "Back to Blog" link's `onclick` reads the `url` query
parameter and assigns it to `location.href`.

## Solution

Visit (or deliver) a URL where `url` points at your exploit server:

```
https://YOUR-LAB-ID.web-security-academy.net/post?postId=4&url=https://YOUR-EXPLOIT-SERVER-ID.web-security-academy.net/
```

Clicking "Back to Blog" sends the victim to your site — lab solved.

## Notes

Client-side redirects validate nothing here; any `url=` value becomes the
navigation target.
