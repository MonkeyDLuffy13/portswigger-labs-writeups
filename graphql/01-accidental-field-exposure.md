# Lab 01 — Accidental exposure of private GraphQL fields

> **Apprentice** · [Official lab](https://portswigger.net/web-security/graphql/lab-graphql-accidental-field-exposure)

**Entry point:** the login mutation · introspection is enabled.

## Solution

1. Send the login request to Repeater → *GraphQL → Set introspection query*
   → save queries to site map.
2. Introspection reveals a `getUser` query returning `username` **and**
   `password`, keyed by `id`.
3. Run it with `id: 1` → administrator's credentials. Log in, delete carlos
   via the admin panel — lab solved.

## Notes

If introspection is disabled, try the suggested-fields trick or common
names (`getUser`, `user(id:)`).
