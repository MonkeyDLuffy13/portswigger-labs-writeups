# Lab 02 — JWT algorithm confusion with no exposed key

> **Expert** · [Official lab](https://portswigger.net/web-security/jwt/algorithm-confusion/lab-jwt-authentication-bypass-via-algorithm-confusion-with-no-exposed-key)

**Entry point:** same confusion — but the public key is **not** published.
Recover it mathematically from two tokens.

## Solution

1. Save **two** valid session JWTs (login, logout, login again).
2. Derive candidate public keys with the provided tool:

```bash
docker run --rm -it portswigger/sig2n <token1> <token2>
```

3. For each candidate it outputs a tampered JWT (X.509 and PKCS1 forms).
   Test each tampered JWT on `/my-account`: a **200** means you found the
   real key (302 = wrong candidate).
4. Take the verified **Base64 X.509 key** → JWT Editor → *New Symmetric
   Key* → paste into `k`.
5. Set `alg: HS256`, `sub: administrator`, **Sign** with the symmetric key
   ("Don't modify header") → `/admin` → delete carlos — lab solved.

## Notes

`sig2n` exploits the fact that with two signatures you can solve for the
modulus candidates of the RSA key.
