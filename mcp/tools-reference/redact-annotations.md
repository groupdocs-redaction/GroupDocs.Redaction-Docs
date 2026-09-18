---
id: mcp-tool-redact-annotations
url: redaction/mcp/tools-reference/redact-annotations
title: redact_annotations
weight: 3
description: "The redact_annotations MCP tool redacts or deletes annotations and comments in a document, replacing matching text or removing them entirely."
keywords: redact_annotations MCP tool, remove comments before sharing, redact sticky notes PDF, delete annotations AI agent
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`redact_annotations` deals with the text people forget: comments, sticky notes, and highlights. Replace matching annotation text with a placeholder, or delete annotations entirely with `deleteAll`. Example prompt: *"Remove all the internal comments before this goes out"*.

**Tool description (as the AI agent sees it):**

> Redacts or deletes annotations (comments, sticky notes, highlights) in a document and saves the result to storage. Can replace matching annotation text with a placeholder, or delete annotations entirely. Call this tool whenever the user asks to redact, remove, hide, or clean up comments or annotations in a document. Do NOT pre-check whether files exist — just pass the filename the user provided. The tool resolves files from storage and returns an error with available files if a name is not found. On failure, the response text starts with 'Annotation redaction failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "redaction/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `pattern` | string | no | Regex pattern to match annotations. Omit to target all annotations. |
| `replacement` | string | no | Replacement text for matched annotation content. Ignored when deleteAll is true (default: '[REDACTED]') |
| `deleteAll` | boolean | no | When true, deletes matched annotations entirely instead of replacing their text (default: false) |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "redact_annotations",
  "arguments": {
    "file": {
      "filePath": "case-file.pdf"
    },
    "deleteAll": true
  }
}
```

## Result

A saved-path message naming the result.

Annotations are a classic redaction miss: the body text gets cleaned, and a reviewer's comment quoting the same name survives in the margin. Run this as part of every redaction pass, not as an afterthought.

On failure the text starts with `Annotation redaction failed for`, followed by the exception type and message.

## Example prompts

* *"Remove all comments and sticky notes before this goes out."*
* *"Redact any annotation mentioning the client name."*
* *"Delete the review annotations but keep the document as is."*
