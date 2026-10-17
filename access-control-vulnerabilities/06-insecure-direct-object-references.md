# Lab 06 — Insecure direct object references

> **Practitioner** · [Official lab](https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references)

**Entry point:** chat transcripts are served as predictable text files
(`/download-transcript/2.txt`).

## Solution

1. Live chat → send a message → **View transcript**: the URL ends in an
   incrementing number (`2.txt`).
2. Change it to `1.txt` — another user's transcript, containing their
   password.
3. Log in with the stolen credentials — lab solved.

## Mitigation

Reference objects by UUIDs *and* verify ownership server-side.
