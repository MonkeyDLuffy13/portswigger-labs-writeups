# Lab 06 — Authentication bypass via flawed state machine

> **Expert** · [Official lab](https://portswigger.net/web-security/logic-flaws/state-machine)

**Entry point:** login requires a role-selection step — skipping it
defaults to the wrong role.

## Solution

1. Content discovery finds `/admin`; visiting it from the role-selector
   page fails.
2. Intercept the login: forward `POST /login`, then **drop** the following
   `GET /role-selector` request.
3. Browse the home page — the state machine defaulted your role to
   **administrator**. `/admin` opens; delete `carlos` — lab solved.

## Mitigation

Define all valid states and transitions; default to the least-privileged
role and reject requests in undefined states.
