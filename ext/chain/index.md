---
layout: page
title: Chain Operations
---

| This document is a work in progress specification.

This extension provides a means to perform chaining "operations" in a linear manner. These operations are used for chain processing such as LLM chains.

```json
POST /chain HTTP/1.1
Host: example.org
Content-Type: application/vnd.api+json;ext="https://jsonapi.org/ext/chain"
Accept: application/vnd.api+json;ext="https://jsonapi.org/ext/chain"

{
  "chain:operations": [{
    "ref": {
      "type": "llm",
      "id": "8k-model"
    },
    "data": {
      "prompt": ""
    }
  }, {
    "ref": {
      "type": "llm",
      "id": "7m-model"
    },
    "data": {
      "prompt": "What happend at {{ data.answer }}?"
    }
  }]
}
```

A server might respond to this request as follows:

```json
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json;ext="https://jsonapi.org/ext/chain"

{
  "data": {
    "answer": "..."
  }
}
```