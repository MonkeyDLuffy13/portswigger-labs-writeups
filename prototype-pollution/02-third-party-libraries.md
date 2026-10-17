# Lab 02 — Client-side prototype pollution in third-party libraries

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/client-side/lab-prototype-pollution-client-side-prototype-pollution-in-third-party-libraries)

**Entry point:** use **DOM Invader** (Burp's built-in browser) to find the
source and the `hitCallback` gadget.

## Solution

1. Burp browser → DOM Invader → enable prototype-pollution detection →
   reload: two vectors found in the URL fragment (`#__proto__[...]`).
2. *Scan for gadgets* → found: `setTimeout()` sink reached via the
   **`hitCallback`** gadget (Google Analytics library).
3. *Exploit* → DOM Invader generates the PoC (`alert(1)`).
4. Deliver to the victim from the exploit server:

```html
<script>
location="https://YOUR-LAB-ID.web-security-academy.net/#__proto__[hitCallback]=alert%28document.cookie%29"
</script>
```

Lab solved.
