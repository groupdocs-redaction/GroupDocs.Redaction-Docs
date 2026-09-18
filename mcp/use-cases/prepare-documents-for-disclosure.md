---
id: mcp-uc-prepare-documents-for-disclosure
url: redaction/mcp/use-cases/prepare-documents-for-disclosure
title: How to prepare documents for disclosure with an AI agent
linkTitle: Prepare documents for disclosure
weight: 2
description: "Prepare documents for legal disclosure or FOI release with an AI agent over MCP: redact text, cover images, clear annotations and metadata, then verify."
keywords: prepare documents for disclosure AI, FOI redaction agent, legal disclosure redaction MCP, remove PII before release
productName: GroupDocs.Redaction MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to prepare documents for disclosure with an AI agent"
        description: "Prepare documents for legal disclosure or FOI release with an AI agent over MCP: redact text, cover images, clear annotations and metadata, then verify."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Redaction MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Take case-file.pdf and prepare it for disclosure: redact all email addresses and the name Jane Smith, delete all annotations, clear the document properties. Apply each step to the file produced by the previous one, and report the match count at every step."
---

Disclosure is where partial redaction becomes a headline. The work is not hard; it is *sequential*, and each step writes a new file.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The order

1. **Text** — [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) for each pattern: names, emails, identifiers, account numbers.
2. **Images** — [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) for signatures, photographs, stamps, and any scanned region.
3. **Annotations** — [`redact_annotations`]({{< ref "redaction/mcp/tools-reference/redact-annotations.md" >}}), usually `deleteAll`, because internal review notes are rarely disclosable.
4. **Metadata** — [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) for author, company, and dates.
5. **Verify** — [Verify a redaction]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}).

## The prompt

> Take case-file.pdf and prepare it for disclosure: redact all email addresses and the name "Jane Smith", delete all annotations, clear the document properties. Apply each step to the file produced by the previous one, and report the match count at every step.

The two clauses at the end are what make the result trustworthy: **chaining** keeps every redaction, and **counts** make each step checkable.

## Why chaining is the failure everyone hits

Each tool writes `<name>_redacted.<ext>`-style output rather than editing in place. An agent that passes the *original* into step 2 produces a document with the image covered and the emails back. The file names in the transcript are your audit trail — read them.

## Multiple patterns

Each pattern is its own [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) call, chained the same way. Ask for them one at a time with counts, rather than as a single opaque instruction: five calls with five numbers is a record; one call with "done" is not.

## Evaluation mode makes this workflow dangerous

One redaction per document, four replacements maximum. A disclosure pass under those limits produces a document that looks processed and still contains the data — and nothing in the responses says so. Make the licence check the first step:

> Before you start: what is the license status of the redaction server?

[`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}); see [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}}).

## Keep the originals separate

The unredacted file still exists, in the same folder, one letter different in the name. Move finished originals out of the working folder, or configure a separate `GROUPDOCS_MCP_OUTPUT_PATH` ([configuration]({{< ref "redaction/net/mcp/configuration.md" >}})) so redacted copies land somewhere distinct. Releasing the wrong file is not a redaction failure, but it fails just as badly.
