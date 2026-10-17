# Lab 07 — Bypassing access controls using email address parsing discrepancies

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/email-address-parsing-discrepancies)

**Entry point:** registration allows only `@ginandjuice.shop` — but the
validator and the mail server **parse encoded emails differently**.

## Solution

1. Plain exploit-domain emails are blocked; encoded-words are detected
   (`=?iso-8859-1?q?...` and `=?utf-8?q?...` rejected).
2. **UTF-7 encoded-words slip through.** Register with:

```
=?utf-7?q?attacker&AEA-[YOUR-EXPLOIT-SERVER-ID]&ACA-?=@ginandjuice.shop
```

(the UTF-7 payload decodes to `attacker@[YOUR-EXPLOIT-SERVER-ID]`)

3. Validation sees `@ginandjuice.shop` at the end; the mail server delivers
   the confirmation to your exploit-server address.
4. Confirm the registration from the email client, log in — lab solved.

## Notes

When two components disagree about parsing (encoded-words, quoting,
comments), authorization based on parsed values can be split-brained.
