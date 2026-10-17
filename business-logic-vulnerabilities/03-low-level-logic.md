# Lab 03 — Low-level logic flaw

> **Practitioner** · [Official lab](https://portswigger.net/web-security/logic-flaws/low-level-logic-flaw)

**Entry point:** the cart total is a signed 32-bit integer (in cents) that
overflows; max 2-digit quantity per request.

## Solution

1. Add the jacket, intercept `POST /cart`; quantity accepts at most **99**
   per request — so automate: Intruder, null payload, *continue
   indefinitely*, `quantity=99`. Refresh the cart until the total flips to a
   huge **negative** number (past 2,147,483,647 cents).
2. Empty the cart and redo it precisely: exactly **323** requests of 99
   (resource pool = 1 concurrent request).
3. In Repeater, add **47** jackets — total lands around **-$1221.96**.
4. Add a cheap item in a small quantity until the total rises into the
   **$0–$100** range (inside your credit).
5. Checkout — lab solved.

## Key values

`99` × 323 bulk requests → 47 jackets → top up with cheap items → total in
[0, 100] dollars.
