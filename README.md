# PortSwigger Labs — Write-ups & Solutions

Personal write-up repository for the
[PortSwigger Web Security Academy](https://portswigger.net/web-security) labs.
One folder per topic; each topic has an index with the full lab table,
official links, and per-lab solution files.

## Topics

| Topic | Labs | Solutions | Index |
|-------|-----:|----------:|-------|
| SQL Injection | 18 | ✅ | [sql-injection/](sql-injection/) |
| Cross-Site Scripting | 33 | ✅ | [cross-site-scripting/](cross-site-scripting/) |
| CSRF | 11 | ✅ | [cross-site-request-forgery-csrf/](cross-site-request-forgery-csrf/) |
| Clickjacking | 6 | ✅ | [clickjacking/](clickjacking/) |
| DOM-based Vulnerabilities | 8 | ✅ | [dom-based-vulnerabilities/](dom-based-vulnerabilities/) |
| CORS | 4 | ✅ | [cross-origin-resource-sharing-cors/](cross-origin-resource-sharing-cors/) |
| XXE | 9 | ✅ | [xml-external-entity-xxe-injection/](xml-external-entity-xxe-injection/) |
| SSRF | 7 | ✅ | [server-side-request-forgery-ssrf/](server-side-request-forgery-ssrf/) |
| HTTP Request Smuggling | 24 | ✅ | [http-request-smuggling/](http-request-smuggling/) |
| OS Command Injection | 6 | ✅ | [os-command-injection/](os-command-injection/) |
| SSTI | 7 | ✅ | [server-side-template-injection/](server-side-template-injection/) |
| Path Traversal | 6 | ✅ | [path-traversal/](path-traversal/) |
| Access Control | 14 | ✅ | [access-control-vulnerabilities/](access-control-vulnerabilities/) |
| Authentication | 15 | ✅ | [authentication/](authentication/) |
| WebSockets | 3 | ✅ | [websockets/](websockets/) |
| Web Cache Poisoning | 13 | ✅ | [web-cache-poisoning/](web-cache-poisoning/) |
| Insecure Deserialization | 10 | ✅ | [insecure-deserialization/](insecure-deserialization/) |
| Information Disclosure | 7 | ✅ | [information-disclosure/](information-disclosure/) |
| Business Logic Vulnerabilities | 12 | ✅ | [business-logic-vulnerabilities/](business-logic-vulnerabilities/) |
| API Testing | 5 | ✅ 5 solutions | [api-testing/](api-testing/) |
| GraphQL API Vulnerabilities | 5 | ✅ 5 solutions | [graphql/](graphql/) |
| JWT Attacks | 8 | ✅ 8 solutions | [jwt/](jwt/) |
| OAuth Authentication | 6 | ✅ 6 solutions | [oauth/](oauth/) |
| File Upload Vulnerabilities | 7 | ✅ 7 solutions | [file-upload/](file-upload/) |
| NoSQL Injection | 4 | ✅ 4 solutions | [nosql-injection/](nosql-injection/) |
| Prototype Pollution | 10 | ✅ 10 solutions | [prototype-pollution/](prototype-pollution/) |
| Web LLM Attacks | 8 | ✅ 8 solutions | [web-llm-attacks/](web-llm-attacks/) |
| Web Cache Deception | 5 | ✅ 5 solutions | [web-cache-deception/](web-cache-deception/) |
| **Total** | **271 labs** | ✅ |

## Tooling — no Burp Pro required

Every write-up is solvable with **Burp Community Edition** plus free tools:

- **Out-of-band labs** (blind XXE, blind SSRF, blind command injection):
  Collaborator is Pro-only — use a free OOB service such as
  [interact.sh](https://interact.sh), [canarytokens.org](https://canarytokens.org)
  (DNS + HTTP) or [webhook.site](https://webhook.site) (HTTP). Each affected
  write-up carries a 🔧 note with the substitution.
- **CSRF PoCs**: built manually from the included HTML forms (the PoC
  generator is Pro-only).
- **Brute-force loops with re-login macros** (2FA brute force, infinite
  money): ready Python scripts are included in the write-ups.
- **Content discovery / comments**: page source review or free tools
  (ffuf/gobuster).
- Free extensions that work in Community: JWT Editor, Param Miner,
  Turbo Intruder, DOM Invader.

## About the lab lists

The initial lab lists came from a personal tracker that contained a handful
of entries with no live lab page; those rows are kept in the tables marked
with an em-dash and a note pointing to the real, live labs of that topic.
Every other row links to a live lab page on portswigger.net. The catalog was built by enumerating the live Academy site directly (273 labs published), so the repository covers every current topic.

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
