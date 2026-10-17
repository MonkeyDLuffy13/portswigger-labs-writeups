# Lab 05 — Authentication bypass via encryption oracle

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/encryption-oracle)

**Entry point:** the `stay-logged-in` cookie is **encrypted** (not signed),
and the comment feature's `notification` cookie acts as an
encrypt/decrypt oracle.

## Solution

1. Invalid comment email → `Set-Cookie: notification=<encrypted>` whose
   decryption is reflected: *"Invalid email address: `<input>`"* — an
   encryption oracle.
2. Decrypt your `stay-logged-in` cookie via the oracle → plaintext is
   `wiener:<timestamp>`.
3. Re-encrypt `administrator:<timestamp>` — the oracle prefixes 23 bytes
   ("Invalid email address: "), so after encrypting, decode the cookie,
   **delete the first 23 bytes** in Burp's Hex editor, re-encode, and let
   the oracle pad the block (duplicate the last block as needed to keep
   16-byte alignment).
4. Set the crafted cookie as `stay-logged-in` → you're `administrator`.
5. Delete `carlos` via `/admin` — lab solved.

## Notes

Encryption without authentication (no MAC) + a decrypting reflection =
full cookie forgery. Always authenticate ciphertexts (encrypt-then-MAC).
