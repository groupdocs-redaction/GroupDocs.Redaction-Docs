---
id: mcp-uc-redact-sensitive-data-with-ai-agents
url: redaction/mcp/use-cases/redact-sensitive-data-with-ai-agents
title: How to redact sensitive data from documents with AI agents
linkTitle: Redact with AI agents
weight: 1
description: "Redact sensitive data from documents with an AI agent over MCP: pattern-based text redaction, area redaction, annotations, and metadata — all locally."
keywords: redact sensitive data AI agent, MCP redaction, Claude redact PDF, remove PII from documents
productName: GroupDocs.Redaction MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to redact sensitive data from documents with AI agents"
        description: "Redact sensitive data from documents with an AI agent over MCP: pattern-based text redaction, area redaction, annotations, and metadata — all locally."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Redaction MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Redact the literal string Acme Holdings everywhere, including in comments."
---

Redaction with an agent works because the division of labour is clear: the **agent** helps you express *"every email address and the client's name"* as patterns and drives the calls; the **engine** applies them exactly, locally, in the document.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The pattern

1. Put the document in the storage folder the server can see.
2. Ask: *"Redact every email address in case-file.pdf and tell me how many you replaced."*
3. The agent calls [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) with a regular expression.
4. A redacted copy appears in your output folder; the original is untouched.
5. You verify — see [Verify a redaction]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}).

## Always ask for the match count

*"Done"* is not a result. *"Replaced 14 matches"* is, because it can be wrong in a way you can notice: if you expected two and got fourteen, the pattern is too loose; if you expected fourteen and got four, you are probably in [evaluation mode]({{< ref "redaction/mcp/getting-started/licensing.md" >}}) with its four-replacement cap.

## The four places data hides

A complete pass is four calls, not one:

| Where | Tool |
|---|---|
| Body text | [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) |
| Scans, photos, signatures | [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) |
| Comments and sticky notes | [`redact_annotations`]({{< ref "redaction/mcp/tools-reference/redact-annotations.md" >}}) |
| Author, company, properties | [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) |

Chain them on the **produced file** each time — every call writes a new document, and applying the second redaction to the original throws away the first.

## Patterns worth keeping

> Redact anything matching `[\w.+-]+@[\w-]+\.[\w.]+` — email addresses.
> Redact `\b\d{3}-\d{2}-\d{4}\b` — US social security numbers.
> Redact the literal string "Acme Holdings" everywhere, including in comments.

Ask the agent to show you the pattern before it runs. A regex you have read is a redaction you can defend.

## Setup

```bash
dnx GroupDocs.Redaction.Mcp --yes
```

with `GROUPDOCS_MCP_STORAGE_PATH` pointing at the folder — [per-client config]({{< ref "redaction/net/mcp/install-in-ai-clients.md" >}}) or the [installer]({{< ref "redaction/mcp/getting-started/_index.md" >}}).

## Where to go next

* [Prepare documents for disclosure]({{< ref "redaction/mcp/use-cases/prepare-documents-for-disclosure.md" >}}) — the full four-tool pass, in order.
* [Redact scanned documents and images]({{< ref "redaction/mcp/use-cases/redact-scanned-documents.md" >}}) — when there is no text layer.
* [Verify a redaction]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}) — proving it, not assuming it.
* [On-premise architecture]({{< ref "redaction/mcp/use-cases/on-premise-redaction.md" >}}) — what leaves the machine, honestly.
