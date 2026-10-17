# Lab 11 — Insufficient workflow validation

> **Practitioner** · [Official lab](https://portswigger.net/web-security/logic-flaws/insufficient-workflow-validation)

**Entry point:** checkout is a sequence — but only the *last* request
confirms the order, and it isn't validated against the cart.

## Solution

1. Buy any cheap item once; note the flow ends with
   `GET /cart/order-confirmation?order-confirmation=true`.
2. Add the leather jacket to the cart (you can't afford it).
3. In Repeater, replay the confirmation request directly — the order
   completes without deducting the cost — lab solved.

## Mitigation

Enforce the workflow server-side: verify state transitions (cart → paid →
confirmed) and that the confirmation matches a completed payment.
