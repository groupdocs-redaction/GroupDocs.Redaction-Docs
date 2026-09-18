---
id: mcp-uc-verify-a-redaction
url: redaction/mcp/use-cases/verify-a-redaction
title: How to verify that a redaction is complete
linkTitle: Verify a redaction
weight: 4
description: "Verify a redaction with an AI agent over MCP: re-run the patterns on the redacted copy, check annotations and metadata, and inspect the pages."
keywords: verify redaction complete, check redacted document AI, test redaction agent, prove document redacted
productName: GroupDocs.Redaction MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to verify that a redaction is complete"
        description: "Verify a redaction with an AI agent over MCP: re-run the patterns on the redacted copy, check annotations and metadata, and inspect the pages."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Redaction MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Run the same email pattern against case-file_redacted.pdf and tell me the match count."
---

A redaction you have not verified is a claim, not a control. Verification costs a few calls and is the difference between *"the tool ran"* and *"the data is gone"*.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## 1. Re-run the pattern on the redacted copy

> Run the same email pattern against case-file_redacted.pdf and tell me the match count.

Expect **zero**. A non-zero count means the pattern missed variants — a different separator, a line break, a different case — or the run hit the evaluation cap.

## 2. Check the other three places

> Now check the redacted copy for annotations and read its document properties.

[`redact_annotations`]({{< ref "redaction/mcp/tools-reference/redact-annotations.md" >}}) and [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) applied in the pass do not prove they were applied to **this** file — the chaining rule means it is entirely possible to verify a document that skipped a step. Check the file you are about to release, not the one you think you produced.

For a deeper metadata check across every package, the [GroupDocs.Metadata MCP server]({{< ref "metadata/mcp/_index.md" >}}) reads EXIF, XMP, and IPTC as well.

## 3. Look at the pages

Area redactions cannot be verified by pattern. Open the document, or have the agent render the affected pages, and confirm each box covers what it was meant to cover — completely, on the right page.

## 4. Confirm the licence state of the run that produced it

> What is the license status of the redaction server?

If the answer is `evaluation`, the redaction was capped at four replacements and the verification above will usually show it — but a document with exactly four matches would pass and still be wrong. Licence first, verify second; both, every time. [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}}).

## Keep the evidence

The verification transcript — patterns used, match counts, files produced, the final zero-match result — is the record that shows the redaction was performed and checked. Ask the agent for it as a summary and keep it with the case file:

> Summarize what you redacted, in which file, with what counts, and what the verification found.

## What verification cannot tell you

It cannot tell you whether your **patterns were the right ones**. Everything above proves that what you asked to be removed is gone. Deciding what should be removed is your judgement, and it remains the part of redaction that no tool takes off your hands.
