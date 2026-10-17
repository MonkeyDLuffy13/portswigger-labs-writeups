# Lab 12 — Weak isolation on dual-use endpoint

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/weak-isolation-on-dual-use-endpoint)

**Entry point:** `POST /my-account/change-password` — optional
`current-password` and a `username` field make it admin-takeover.

## Solution

1. Change your own password; in Repeater, **remove the `current-password`
   parameter** → the change succeeds without the current password.
2. The endpoint also accepts a `username` parameter — set
   `username=administrator` and choose a new password.
3. Log in as `administrator` with it, open `/admin`, delete `carlos` —
   lab solved.

## Mitigation

Optional verification parameters are a classic flaw: require the current
password, ignore client-supplied usernames, and check that the requester
owns the account being modified.
