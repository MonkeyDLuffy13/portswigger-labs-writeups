# Lab 05 — Accessing private GraphQL posts

> **Apprentice** · [Official lab](https://portswigger.net/web-security/graphql/lab-graphql-reading-private-posts)

**Entry point:** `POST /graphql/v1` — blog posts carry sequential ids and
post 3 is missing (hidden).

## Solution

1. Introspection (Repeater → *GraphQL → Set introspection query*) shows the
   `BlogPost` type has a `postPassword` field.
2. In the GraphQL tab, set the query variable `id: 3` and add
   `postPassword` to the requested fields.
3. The response returns the hidden post's password — submit it —
   lab solved.

## Notes

The API returns fields it never renders client-side — always introspect for
fields the UI doesn't use.
