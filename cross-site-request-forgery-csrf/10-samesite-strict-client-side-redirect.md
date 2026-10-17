# Lab 10 — SameSite Strict bypass via client-side redirect

> **Expert** · [Official lab](https://portswigger.net/web-security/csrf/bypassing-samesite-restrictions/lab-samesite-strict-bypass-via-client-side-redirect)

**Entry point:** cookies are `SameSite=Strict` — but a **same-site**
client-side redirect chain can be abused as a gadget.

## Solution

1. Gadget: after posting a comment, `/post/comment/confirmation?postId=N`
   redirects the user via JavaScript (`commentConfirmationRedirect.js`)
   building the target from `postId` — path traversal allowed:
   `postId=1/../../my-account` lands on your account page, cookie attached
   (it's same-site).
2. The email-change endpoint also accepts **GET** (use Burp's "Change
   request method").
3. Final exploit — navigate the victim through the gadget with the email
   request embedded (note the encoded `&`):

```html
<script>
document.location = "https://YOUR-LAB-ID.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=pwned%40evil-you.net%26submit=1";
</script>
```

4. Deliver to victim — the same-site client redirect carries the Strict
   cookie and executes the change — lab solved.

## Notes

SameSite protects cross-site requests, not cross-site pages that abuse
on-site redirectors. Audit client-side redirects as CSRF gadgets.
