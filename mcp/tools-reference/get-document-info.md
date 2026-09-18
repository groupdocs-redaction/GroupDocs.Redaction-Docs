---
id: mcp-tool-get-document-info
url: redaction/mcp/tools-reference/get-document-info
title: get_document_info
weight: 5
description: "The get_document_info MCP tool returns file type, page count, size, and per-page dimensions — useful for placing an area redaction accurately."
keywords: get_document_info MCP, page dimensions for redaction, inspect document before redacting, MCP document info
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`get_document_info` returns the file type, page count, size, and **per-page dimensions** — the numbers you need before placing an area redaction. Example prompt: *"How big is page 2? I need to cover the bottom third."*

**Tool description (as the AI agent sees it):**

> Returns the file type, page count, size, and per-page dimensions of a document as JSON, without modifying the file. Supports PDF, DOCX, XLSX, PPTX, images, and 30+ more document formats. Call this tool whenever the user asks to inspect a document, check its page count, or get its details — useful as a precondition before redacting (e.g. to read page width/height before choosing redact_image_area coordinates). Do NOT pre-check whether the file exists — just pass the filename the user provided. Returns a JSON object with fields `fileName`, `fileType`, `pageCount`, `size`, and `pages` (array of `{ number, width, height }`). On failure, the response text starts with 'Document-info lookup failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "redaction/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "get_document_info",
  "arguments": {
    "file": {
      "filePath": "case-file.pdf"
    }
  }
}
```

## Result

A JSON object with `fileName`, `fileType`, `pageCount`, `sizeBytes`, and `pages` (width and height per page).

Per-page dimensions turn *"cover the bottom third of page 2"* into concrete `x`/`y`/`width`/`height` values for [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}).

On failure the text starts with `Document-info lookup failed for`, followed by the exception type and message.

## Example prompts

* *"How many pages, and how big is each one?"*
* *"What are the dimensions of page 2?"*
* *"Is this a PDF or a Word document?"*
