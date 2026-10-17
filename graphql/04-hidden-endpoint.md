# Lab 04 — Finding a hidden GraphQL endpoint

> **Practitioner** · [Official lab](https://portswigger.net/web-security/graphql/lab-graphql-find-the-endpoint)

**Entry point:** the GraphQL endpoint isn't referenced anywhere — find and
query it at `/api`.

## Solution

1. Probe common suffixes: `GET /api` → *"Query not present"* — a GraphQL
   responder.
2. Universal query as a URL parameter:

```
/api?query=query{__typename}
```

→ `{"data":{"__typename":"query"}}` — confirmed.

3. Send the introspection query (URL-encoded) — the response is truncated:
   the blocklist rejects introspection containing `meta`. Bypass with a
   ** aliased/duplicated version** — e.g. reuse the introspection query but
   rename fields with aliases, or use the `__schema` query with each field
   aliased (`a: __schema {...}`) so the filter doesn't match — the schema is
   revealed, exposing the hidden data — lab solved.

## Notes

Introspection blocklists that match keywords are bypassed by aliasing every
field — the response shape is identical.
