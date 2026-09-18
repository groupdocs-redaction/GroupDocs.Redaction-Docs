---
id: mcp-uc-redact-scanned-documents
url: redaction/mcp/use-cases/redact-scanned-documents
title: How to redact scanned documents and images with an AI agent
linkTitle: Redact scans and images
weight: 3
description: "Redact scanned documents and images with an AI agent over MCP using area redaction, and understand why text redaction finds nothing in a scan."
keywords: redact scanned document AI, black out area PDF agent, redact image MCP, hide face in scan
productName: GroupDocs.Redaction MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to redact scanned documents and images with an AI agent"
        description: "Redact scanned documents and images with an AI agent over MCP using area redaction, and understand why text redaction finds nothing in a scan."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Redaction MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "How big is page 2?"
---

A scan is a picture of a document. The words on it are pixels, so pattern matching has nothing to match — [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) returns zero matches on a scanned page, and **zero matches is not the same as nothing sensitive**.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The tool for this

[`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) covers a rectangle with a solid colour box, permanently. Coordinates are pixels from the top-left corner of the page.

## Getting the coordinates

> How big is page 2?

[`get_document_info`]({{< ref "redaction/mcp/tools-reference/get-document-info.md" >}}) returns per-page width and height, which turns *"the bottom third"* into real numbers. Then:

> Cover the bottom third of page 2 with a black box.

For a specific element — a signature, a face, a header — you need its position. Two practical routes: open the page in any viewer and read the coordinates, or render a preview with a tool that can (the [GroupDocs.Annotation MCP server](/annotation/mcp/) can return page images inline) and let a vision-capable model estimate the box.

## Always check the result visually

An area redaction that is 20 pixels short is a redaction that failed, and no response text will tell you. Look at the page. This is the one redaction case where verification cannot be automated by re-running a pattern — the check is your eyes, or a preview the agent can see.

## Mixed documents

Many PDFs are part text, part scan: a born-digital contract with a scanned signature page. Run both tools:

> Redact the email addresses across the whole document, then cover the signature block on page 7, applying the second step to the result of the first.

## Why there is no OCR here

This server redacts; it does not recognise text in images. That keeps the behaviour predictable — there is no confidence threshold quietly deciding that a blurry name was not a name. If your workflow needs text out of scans, extract it first with a tool built for it, decide what is sensitive, then redact by area.

## The evaluation limit applies here too

One redaction per document in evaluation mode means one box. A page needing three covered regions gets one — and looks processed. [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) first.
