# PortSwigger Labs — Write-ups & Solutions

Personal write-up repository for the
[PortSwigger Web Security Academy](https://portswigger.net/web-security) labs.
One folder per topic; each topic has an index with the full lab table,
official links, and per-lab solution files.

## Topics

| Topic | Tracker labs | Verified live | Solved | Index |
|-------|-------------:|--------------:|--------|-------|
| SQL Injection | 21 | 18 | ✅  | [sql-injection/](sql-injection/) |
| Cross-Site Scripting | 18 | 15 | ✅ | [cross-site-scripting/](cross-site-scripting/) |
| CSRF | 5 | 5 | ✅ | [cross-site-request-forgery-csrf/](cross-site-request-forgery-csrf/) |
| Clickjacking | 3 | 2 | ✅ | [clickjacking/](clickjacking/) |
| DOM-based Vulnerabilities | 3 | 2 | ✅ | [dom-based-vulnerabilities/](dom-based-vulnerabilities/) |
| CORS | 4 | 3 | ✅ | [cross-origin-resource-sharing-cors/](cross-origin-resource-sharing-cors/) |
| XXE | 4 | 4 | ✅ | [xml-external-entity-xxe-injection/](xml-external-entity-xxe-injection/) |
| SSRF | 3 | 3 | ✅ | [server-side-request-forgery-ssrf/](server-side-request-forgery-ssrf/) |
| HTTP Request Smuggling | 4 | 2 | ✅ | [http-request-smuggling/](http-request-smuggling/) |
| OS Command Injection | 4 | 3 | ✅ | [os-command-injection/](os-command-injection/) |
| SSTI | 6 | 6 | ✅ | [server-side-template-injection/](server-side-template-injection/) |
| Path Traversal | 6 | 6 | ✅ | [path-traversal/](path-traversal/) |
| Access Control | 5 | 5 | ✅ | [access-control-vulnerabilities/](access-control-vulnerabilities/) |
| Authentication | 5 | 4 | ✅ | [authentication/](authentication/) |
| WebSockets | 2 | 2 | ✅ | [websockets/](websockets/) |
| Web Cache Poisoning | 5 | 5 | ✅ | [web-cache-poisoning/](web-cache-poisoning/) |
| Insecure Deserialization | 5 | 5 | ✅ | [insecure-deserialization/](insecure-deserialization/) |
| Information Disclosure | 5 | 3 | ✅ | [information-disclosure/](information-disclosure/) |
| Business Logic Vulnerabilities | 4 | 4 | ✅ | [business-logic-vulnerabilities/](business-logic-vulnerabilities/) |
| **Total** | **112** | **97** | **97** | |

## About the lab lists

The lab lists came from a personal tracker (`data.json`) that turned out to
contain **15 entries that do not exist on the live Academy** (e.g. *H2.TE /
TE.H2 request smuggling*, *"OS command injection with filter bypass"*,
*"CORS vulnerability with trusted subdomains"*, several CSP XSS variants).
Every URL in this repository was **link-checked on 2026-10-17**: each resolved
link returned HTTP 200 **and** its page title matches the lab name. Ghost
entries are kept in the tables (marked `—`) with a ⚠️ note pointing to the
real, live labs of that topic — so the tracker stays honest.

## Repository Structure

```
.
├── data.json                # the original personal tracker (valid-JSON copy, 19 topics / 112 labs)
├── <topic>/                 # one folder per topic
│   ├── README.md            # lab table (verified links) + notes
│   └── NN-*.md              # solution files (SQL injection: all 18 done)
└── _TEMPLATE.md             # template for new write-ups
```

## Disclaimer

- These write-ups are published **for educational purposes only**, documenting
  techniques learned while solving the Academy's intentionally vulnerable
  training labs.
- Do not apply any technique described here to systems you do not have
  explicit permission to test.

## License

Code snippets and payloads are released under the [MIT License](LICENSE).
Write-up text: all rights reserved by the author.
