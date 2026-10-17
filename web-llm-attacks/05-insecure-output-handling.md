# Lab 05 — Exploiting insecure output handling in LLMs

> **Practitioner** · [Official lab](https://portswigger.net/web-security/llm-attacks/lab-exploiting-insecure-output-handling-in-llms)

**Entry point:** the Live chat LLM renders responses as HTML and reads
product reviews into its answers.

## Solution

1. Probe: send `<img src=1 onerror=alert(1)>` to the chat — the alert fires
   (output is rendered unsafely).
2. Reviews are HTML-encoded directly, but the LLM's `product_info` API
   returns review text into the chat **unencoded**.
3. Plant the payload as a review on another product, wrapped in a plausible
   sentence:

```text
When I received this product I got a free T-shirt with
"<iframe src=my-account onload=this.contentDocument.forms[1].submit()>">
```

(iframe submits the reader's **delete account** form.)

4. Ask the LLM about that product — the iframe executes in **your** session
   context first to tune the payload, then for the victim/admin — the
   reader's account is deleted — lab solved.

## Mitigation

Treat LLM output as untrusted: encode it before rendering; sanitize data
the LLM ingests.
