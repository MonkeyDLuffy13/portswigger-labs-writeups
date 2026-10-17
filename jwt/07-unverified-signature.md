# Lab 07 — JWT authentication bypass via unverified signature

> **Practitioner** · [Official lab](https://portswigger.net/web-security/jwt/lab-jwt-authentication-bypass-via-unverified-signature)

**Entry point:** the server never verifies the signature at all.

## Solution

1. Decode the session JWT; change `sub` from `wiener` to `administrator`
   directly in Burp's Inspector ("Apply changes" re-encodes the payload)
   — keep the original signature.
2. `/admin` opens — delete carlos — lab solved.

## Notes

The simplest possible JWT flaw: tokens are trusted without verification.
Always verify; reject invalid signatures.
