---
id: mcp-tools-reference
url: redaction/mcp/tools-reference
title: Tools reference
weight: 2
description: "Complete reference of every tool the GroupDocs.Redaction MCP server exposes to AI agents, with parameters, example prompts, and results."
keywords: MCP tools list redaction, redact_text MCP tool, redact image area MCP, erase metadata MCP, MCP tools reference
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

Complete reference of every tool the GroupDocs.Redaction MCP server exposes to AI agents, with parameters, example prompts, and results. Captured from a live `tools/list` call against server version **26.9.0** (raw capture: `tools-list.generated.json` in this section's source).

| Tool | What it does |
|---|---|
| [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) | Redacts text matching a regular expression and saves a redacted copy |
| [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) | Covers a rectangular page area with a solid box, hiding image content |
| [`redact_annotations`]({{< ref "redaction/mcp/tools-reference/redact-annotations.md" >}}) | Redacts or deletes annotations and comments |
| [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) | Erases metadata fields that carry identifying information |
| [`get_document_info`]({{< ref "redaction/mcp/tools-reference/get-document-info.md" >}}) | Returns file type, page count, size, and per-page dimensions |
| [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) | Reports the active licensing mode and, under metered licensing, consumption |

## The FileInput shape

Every tool takes its document through the same `file` object — pass **either** a name from your storage folder **or** inline content:

```json
{ "file": { "filePath": "case-file.pdf" } }
```

| Field | Type | Description |
|---|---|---|
| `filePath` | string | File path or name in the configured storage folder |
| `fileContent` | string | Base64-encoded file content (alternative to `filePath`) |
| `fileName` | string | Original filename with extension — required with `fileContent`. Since **26.9.0** it also works on its own, resolved from the storage folder exactly like `filePath` |

You rarely write this JSON yourself: the AI agent does, from your plain-language prompt. Missing files are not an error to fear — the tool responds with the list of available files so the agent can correct itself.
