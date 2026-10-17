# Lab 07 — Multi-step process with no access control on one step

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-multi-step-process-with-no-access-control-on-one-step)

**Entry point:** role upgrade is a 2-step form; one step skips the check.

## Solution

1. As admin, upgrade `carlos` and capture **both** requests.
2. Replay the **confirmation** request (`POST /admin-roles` second step,
   the one containing the confirmed action) with the non-admin session
   cookie, `username=wiener`.
3. The step lacking authorization executes — wiener is admin — lab solved.

## Mitigation

Authorize the operation at execution time on every step, not at the start
of the wizard.
