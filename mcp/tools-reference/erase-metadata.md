---
id: mcp-tool-erase-metadata
url: redaction/mcp/tools-reference/erase-metadata
title: erase_metadata
weight: 4
description: "The erase_metadata MCP tool erases metadata fields — author, title, company, keywords, dates — that carry identifying information."
keywords: erase_metadata MCP tool, remove author metadata redaction, clean document properties before disclosure, PII metadata removal
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`erase_metadata` clears metadata fields that carry identifying information — author, title, company, keywords, dates. The third place data hides, after the body text and the annotations. Example prompt: *"Clear the document properties too"*.

**Tool description (as the AI agent sees it):**

> Erases metadata fields from a document (author, title, company, keywords, dates, etc.) and saves the cleaned file to storage. Use to remove personally identifiable or confidential information embedded in document properties before sharing. Call this tool whenever the user asks to erase, strip, clean, or remove metadata from a document. Accepted fields (comma-separated): All, Author, Title, Subject, Category, Keywords, Description, Creator, Producer, CreatedTime, LastPrinted, LastSavedTime, TotalEditingTime, NameOfApplication, Manager, Company, ContentStatus, Version, Revision, HyperlinkBase, ContentType, Template. Default is All. Do NOT pre-check whether files exist — just pass the filename the user provided. The tool resolves files from storage and returns an error with available files if a name is not found. On failure, the response text starts with 'Metadata erasure failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "redaction/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `fields` | string | no | Comma-separated metadata fields to erase (default: 'All'). E.g. 'Author,Company,CreatedTime' |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "erase_metadata",
  "arguments": {
    "file": {
      "filePath": "case-file.pdf"
    }
  }
}
```

## Result

A saved-path message naming the cleaned file. Pass `fields` to target specific ones; omit it to clear the standard identifying set.

A redaction that stops at the visible page leaves the author's name in the properties — which is exactly the detail that gets noticed. For a full metadata audit across every package (EXIF, XMP, IPTC and more), the [GroupDocs.Metadata MCP server]({{< ref "metadata/mcp/_index.md" >}}) goes deeper; this tool covers the fields that matter for a disclosure pass.

On failure the text starts with `Metadata erasure failed for`, followed by the exception type and message.

## Example prompts

* *"Clear the document properties before I send this."*
* *"Erase the author and company fields."*
* *"Remove metadata as part of the redaction pass."*
