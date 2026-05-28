---
title: Model Context Protocol (MCP) | AI Coding Glossary
source: https://realpython.com/ref/ai-coding-glossary/mcp/
author:
  - "[[Real Python]]"
published: 2026-05-14
created: 2026-05-26
description: An open, client-server communication standard that lets AI applications connect to external tools and data sources.
tags:
  - mcp
  - "#glossary"
---
## Model Context Protocol (MCP)

**Model Context Protocol (MCP)** is an open, client-server communication standard that lets [AI](https://realpython.com/ref/ai-coding-glossary/ai/) applications connect to external tools, resources, and predefined [prompts](https://realpython.com/ref/ai-coding-glossary/prompt/) through a consistent interface.

MCP defines how a client discovers and invokes server-provided capabilities:

- **Tools** are callable actions or API requests that the client can ask the server to perform.
- **Resources** are structured data or context, such as files, database tables, documents, and schemas, accessible by URI, which the client or model can reference.
- **Prompts** are predefined prompt templates that clients can fetch, fill with arguments, and execute to drive structured interactions with language models.

MCP encodes messages using [JSON](https://realpython.com/ref/glossary/json/) -RPC 2.0 over standard transports such as standard input/output (stdio) or streamable HTTP.

The goal is interoperability and portability across assistants, hosts, and integrations, so developers can build a connector once and reuse it in many AI apps.