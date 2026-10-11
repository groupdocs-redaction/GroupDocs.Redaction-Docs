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
          text: "How big is scan.png?"
---

A scan is a picture of a document. The words on it are pixels, so pattern matching has nothing to match — [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) finds nothing to replace on a scanned page, and **finding nothing is not the same as nothing sensitive**.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The tool for this

[`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) covers a rectangle with a solid colour box, permanently. Coordinates are pixels from the top-left corner of the page.

## Getting the coordinates

> How big is scan.png?

[`get_document_info`]({{< ref "redaction/mcp/tools-reference/get-document-info.md" >}}) returns per-page width and height, which turns *"the bottom third"* into real numbers. Then:

> Cover the bottom third of scan.png with a black box.

The tool takes no page argument — only the file and the rectangle — so check where the box landed on every page of the output.

For a specific element — a signature, a face, a header — you need its position. Two practical routes: open the page in any viewer and read the coordinates, or render a preview with a tool that can (`render_page` on the [GroupDocs.Viewer MCP server](/viewer/mcp/) returns page images inline) and let a vision-capable model estimate the box.

## Always check the result visually

An area redaction that is 20 pixels short is a redaction that failed, and no response text will tell you. Look at the page. This is the one redaction case where verification cannot be automated by re-running a pattern — the check is your eyes, or a preview the agent can see.

## Mixed documents

Many PDFs are part text, part scan: a born-digital contract with a scanned signature page. Run both tools:

> Redact the email addresses in contract.docx, then tell me which saved file to use for the next step.

Because `redact_image_area` cannot be aimed at one page, treat scanned pages as images that get their own area redaction, and check every page of the final output.

## Platform limit

On Linux, including the Docker image (a Linux container), `redact_image_area` and `erase_metadata` currently fail on PDF files because the PDF engine's image handling depends on `System.Drawing`, which .NET supports only on Windows; both work on Word documents, and `redact_text` works on PDF. Run PDF area redaction and metadata erasure on Windows with `dnx`.

## Why there is no OCR here

This server redacts; it does not recognise text in images. That keeps the behaviour predictable — there is no confidence threshold quietly deciding that a blurry name was not a name. If your workflow needs text out of scans, extract it first with a tool built for it, decide what is sensitive, then redact by area.

## The evaluation limit applies here too

One redaction per document in evaluation mode means one box. A page needing three covered regions gets one — and looks processed. [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) first.

## Read more

* [Redacting scanned documents when there is no text to find](https://blog.groupdocs.com/redaction/redact-scanned-documents-images-ai-agent-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

