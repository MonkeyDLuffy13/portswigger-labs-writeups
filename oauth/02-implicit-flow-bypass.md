# Lab 02 — Authentication bypass via OAuth implicit flow

> **Expert** · [Official lab](https://portswigger.net/web-security/oauth/lab-oauth-authentication-bypass-via-oauth-implicit-flow)

**Entry point:** the implicit flow hands the user's identity to the client,
which trusts it without verifying the token.

## Solution

1. Study the flow: after OAuth, the blog logs you in by POSTing the profile
   data (email + token) to its own `/authenticate`.
2. In Repeater, change the email in `POST /authenticate` to
   `carlos@carlos-montoya.net` → accepted (the token is never checked
   against the email).
3. Right-click → *Request in browser → In original session* — you're logged
   in as carlos — lab solved.

## Mitigation

Never log users in based on client-asserted identity claims; validate the
access token server-side (or use code flow + PKCE) and verify the token's
`sub` maps to the account.
