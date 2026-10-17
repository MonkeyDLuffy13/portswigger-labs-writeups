# Lab 09 — Inconsistent handling of exceptional input

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/exceptional-input)

**Entry point:** newsletter signup stores the email in an oversized JSON
"blob"; a username **longer than the blob** truncates and overwrites it.

## Solution

1. The comment system serializes metadata into a JSON blob keyed by the
   newsletter email; exceptional input (very long) breaks the parse and the
   app falls back to defaults for that field.
2. Register the newsletter account with an email containing **an absurdly
   long username** so the JSON exceeds its storage limit and gets
   truncated — the stored comment metadata loses the newsletter flag /
   becomes malformed.
3. Post the comment that the lab's exceptional path protects; the
   truncated metadata makes the application treat it as privileged.
4. Complete the lab's stated goal (the page's banner email client shows
   the confirmation) — lab solved.

## Notes

"Exceptional input" (huge, malformed, weird encodings) often takes a
different code path — test lengths beyond field limits and JSON
edge cases.
