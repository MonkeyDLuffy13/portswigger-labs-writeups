# Lab 02 — Exploiting AI agents to trigger secondary vulnerabilities

> **Expert** · [Official lab](https://portswigger.net/web-security/llm-attacks/ai-powered-scanner-vulnerabilities/lab-exploiting-target-website-vulnerabilities-to-bypass-restrictions)

**Entry point:** the AI scanner processes your reviews — use it to trigger a
secondary vulnerability (stored XSS) that the site's own restrictions would
normally block.

## Solution

1. Identify the secondary flaw: e.g. an endpoint/render path where the
   scanner's actions are stored without the same encoding as user input.
2. Inject an indirect prompt into a review instructing the agent to perform
   the action that plants the payload (e.g. call the site's API to submit
   content that reaches a DOM sink), escaping restrictions that apply only
   to direct user input.
3. When the scanner's agent executes the instruction, the payload is stored
   and executes in other users' browsers — lab solved.

## Notes

Treat the LLM agent as an authenticated user you can puppeteer: any API it
can call is an injection primitive.
