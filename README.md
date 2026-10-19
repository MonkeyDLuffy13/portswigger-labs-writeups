# PortSwigger Labs — Write-ups & Solutions

Personal write-up repository for the PortSwigger Web Security Academy labs.
One folder per topic; each topic has an index with the full lab table, official
links, and per-lab solution files.

## Topics

| Topic | Labs | Index |
|-------|-----:|-------|
| SQL Injection | 18 | [sql-injection/](sql-injection/) |
| Cross-Site Scripting (XSS) | 30 | [cross-site-scripting/](cross-site-scripting/) |
| Cross-Site Request Forgery (CSRF) | 11 | [cross-site-request-forgery-csrf/](cross-site-request-forgery-csrf/) |
| Clickjacking | 5 | [clickjacking/](clickjacking/) |
| DOM-based Vulnerabilities | 7 | [dom-based-vulnerabilities/](dom-based-vulnerabilities/) |
| CORS | 3 | [cross-origin-resource-sharing-cors/](cross-origin-resource-sharing-cors/) |
| XXE Injection | 9 | [xml-external-entity-xxe-injection/](xml-external-entity-xxe-injection/) |
| SSRF | 7 | [server-side-request-forgery-ssrf/](server-side-request-forgery-ssrf/) |
| HTTP Request Smuggling | 22 | [http-request-smuggling/](http-request-smuggling/) |
| OS Command Injection | 5 | [os-command-injection/](os-command-injection/) |
| SSTI | 7 | [server-side-template-injection/](server-side-template-injection/) |
| Path Traversal | 6 | [path-traversal/](path-traversal/) |
| Access Control | 13 | [access-control-vulnerabilities/](access-control-vulnerabilities/) |
| Authentication | 14 | [authentication/](authentication/) |
| WebSockets | 3 | [websockets/](websockets/) |
| Web Cache Poisoning | 13 | [web-cache-poisoning/](web-cache-poisoning/) |
| Insecure Deserialization | 10 | [insecure-deserialization/](insecure-deserialization/) |
| Information Disclosure | 5 | [information-disclosure/](information-disclosure/) |
| Business Logic Vulnerabilities | 12 | [business-logic-vulnerabilities/](business-logic-vulnerabilities/) |
| HTTP Host Header Attacks | 7 | [host-header-attacks/](host-header-attacks/) |
| OAuth Authentication | 6 | [oauth/](oauth/) |
| File Upload Vulnerabilities | 7 | [file-upload/](file-upload/) |
| JWT Attacks | 8 | [jwt/](jwt/) |
| Essential Skills | 2 | [essential-skills/](essential-skills/) |
| Prototype Pollution | 10 | [prototype-pollution/](prototype-pollution/) |
| GraphQL API Vulnerabilities | 5 | [graphql/](graphql/) |
| Race Conditions | 6 | [race-conditions/](race-conditions/) |
| NoSQL Injection | 4 | [nosql-injection/](nosql-injection/) |
| API Testing | 5 | [api-testing/](api-testing/) |
| Web LLM Attacks | 8 | [web-llm-attacks/](web-llm-attacks/) |
| Web Cache Deception | 5 | [web-cache-deception/](web-cache-deception/) |
| **Total** | **273 labs · 31 topics** | |

## About the lab lists

The initial lab lists came from a personal tracker that contained a handful
of entries with no live lab page; those rows are kept in the topic tables
marked with an em-dash and a note pointing to the real, live labs of that
topic. Every other row links to a live lab page on portswigger.net. The
catalog was built by enumerating the live Academy site directly (273 labs
published), so the repository covers every current topic.

## Repository Structure

```
.
├── <topic>/                 # one folder per topic
│   ├── README.md            # lab table (verified links) + notes
│   └── NN-*.md              # solution files (274 full write-ups)
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
