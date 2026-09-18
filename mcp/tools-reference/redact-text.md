---
id: mcp-tool-redact-text
url: redaction/mcp/tools-reference/redact-text
title: redact_text
weight: 1
description: "The redact_text MCP tool redacts text matching a regular expression from a document and saves a redacted copy, permanently removing the matched content."
keywords: redact_text MCP tool, redact PDF text AI agent, remove SSN from document, regex redaction MCP
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`redact_text` finds text matching a **regular expression** and redacts it, saving a redacted copy. This is the core tool: email addresses, national IDs, phone numbers, account numbers, names — anything you can express as a pattern. Example prompt: *"Redact every email address in case-file.pdf"*.

**Tool description (as the AI agent sees it):**

> Redacts text matching a regex pattern from a document and saves the redacted file to storage. Use to permanently hide sensitive data like SSNs, emails, phone numbers, or any custom pattern. Call this tool immediately whenever the user asks to redact, hide, remove, or black out text in a document. Do NOT pre-check whether files exist — just pass the filename the user provided. The tool resolves files from storage and returns an error with available files if a name is not found. On failure, the response text starts with 'Text redaction failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "redaction/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `pattern` | string | yes | Regex pattern to match text for redaction, e.g. '\d{3}-\d{2}-\d{4}' for SSN |
| `replacement` | string | no | Replacement text (default: '[REDACTED]') |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "redact_text",
  "arguments": {
    "file": {
      "filePath": "case-file.pdf"
    },
    "pattern": "[\\w.+-]+@[\\w-]+\\.[\\w.]+",
    "replacement": "[REDACTED]"
  }
}
```

## Result

A saved-path message naming the redacted file.

The matched text is **replaced in the document**, not covered with a drawn rectangle — which is what makes this redaction rather than obscuring. `replacement` controls what appears in its place; a consistent marker like `[REDACTED]` makes the result reviewable.

Two things to be deliberate about: a pattern that is too loose removes more than you meant, and a pattern that is too tight leaves data behind. Ask the agent to report the **match count**, and verify afterwards.

On failure the text starts with `Text redaction failed for`, followed by the exception type and message.

## Example prompts

* *"Redact every email address in this document."*
* *"Replace all phone numbers with [REDACTED]."*
* *"Redact the client's name everywhere it appears."*
* *"Remove anything matching our account-number format."*

See it used end-to-end: [Redact sensitive data with AI agents]({{< ref "redaction/mcp/use-cases/redact-sensitive-data-with-ai-agents.md" >}}).
