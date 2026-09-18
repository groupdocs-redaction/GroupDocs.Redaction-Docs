---
id: mcp-tool-redact-image-area
url: redaction/mcp/tools-reference/redact-image-area
title: redact_image_area
weight: 2
description: "The redact_image_area MCP tool covers a rectangular area of a page with a solid colour box, permanently hiding image content such as faces, signatures, or stamps."
keywords: redact_image_area MCP tool, black out area of PDF, hide face in document AI, cover signature redaction
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`redact_image_area` covers a rectangle with a solid-colour box, permanently hiding whatever is underneath — a face, a signature, a stamp, a region of a scan. Coordinates are in **pixels from the top-left of the page**. Example prompt: *"Cover the signature block at the bottom of page 2"*.

**Tool description (as the AI agent sees it):**

> Covers a rectangular area of a document page with a solid-color box, permanently hiding image content (e.g. faces, signatures, stamps). Coordinates are in pixels from the top-left corner of the page. Call this tool whenever the user asks to hide, cover, or black out an image area or region in a document. Do NOT pre-check whether files exist — just pass the filename the user provided. The tool resolves files from storage and returns an error with available files if a name is not found. On failure, the response text starts with 'Image area redaction failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "redaction/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `x` | integer | yes | X coordinate (pixels) of the top-left corner of the area to redact |
| `y` | integer | yes | Y coordinate (pixels) of the top-left corner of the area to redact |
| `width` | integer | yes | Width (pixels) of the area to redact |
| `height` | integer | yes | Height (pixels) of the area to redact |
| `color` | string | no | Fill color for the redaction box — named color (e.g. 'Black', 'Red') or hex (e.g. '#FF0000'). Default: 'Black' |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "redact_image_area",
  "arguments": {
    "file": {
      "filePath": "case-file.pdf"
    },
    "x": 100,
    "y": 640,
    "width": 300,
    "height": 120,
    "color": "black"
  }
}
```

## Result

A saved-path message naming the redacted file.

This is the tool for content that has no text layer. Getting the coordinates right is the practical difficulty: use [`get_document_info`]({{< ref "redaction/mcp/tools-reference/get-document-info.md" >}}) for the page dimensions, and check the result visually before relying on it — a box that is 20 pixels too small is a redaction that failed.

On failure the text starts with `Image area redaction failed for`, followed by the exception type and message.

## Example prompts

* *"Cover the signature block at the bottom of page 2."*
* *"Black out the photo in the top-right corner."*
* *"Hide the stamp area on the first page."*
