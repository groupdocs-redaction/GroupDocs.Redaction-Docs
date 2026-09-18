---
id: mcp-supported-formats
url: redaction/mcp/supported-formats
title: Supported formats
weight: 4
description: "The MCP server exposes the full GroupDocs.Redaction engine: PDF, Word, Excel, PowerPoint, images and 30+ more formats can be redacted through your AI agent."
keywords: MCP server supported formats, redact pdf MCP, redact docx MCP, redact images MCP, redaction formats
productName: GroupDocs.Redaction MCP Server
toc: True
---

The MCP server exposes the **full GroupDocs.Redaction engine**: every format the .NET library can redact — 30+ document, spreadsheet, presentation, and image formats — is available to your AI agent. The canonical matrix lives in the library documentation: [supported document formats]({{< ref "redaction/net/getting-started/supported-document-formats.md" >}}).

What matters per family:

* **PDF** — the disclosure format. Text redaction, area redaction, annotations, and metadata all apply.
* **DOCX / XLSX / PPTX** — redact in the working format, including comments, which is where review notes hide.
* **Images and scans** — no text layer, so [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) with coordinates is the tool. There is **no OCR** in this server: text inside a picture is pixels, not text.

**The format decides which tools apply.** On a born-digital PDF, [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) does most of the work. On a scanned one, it will find nothing to match — an empty result there means "no text layer", not "nothing sensitive". That distinction is the single most important thing to get right before trusting a redaction, and it is why [verification]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}) is a step rather than an option.
