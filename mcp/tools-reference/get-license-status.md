---
id: mcp-tool-get-license-status
url: redaction/mcp/tools-reference/get-license-status
title: get_license_status
weight: 6
description: "The get_license_status MCP tool reports which licensing mode the server is running in — evaluation, license file, or metered — and how much metered credit has been consumed."
keywords: get_license_status MCP, check MCP server license, metered consumption MCP, MCP evaluation mode check
productName: GroupDocs.Redaction MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`get_license_status` reports how this server is licensed and, under metered licensing, how much has been consumed. **On a redaction server this is a safety check, not a formality** — evaluation mode caps a redaction at four replacements. Example prompt: *"Is the redaction server licensed?"*

**Tool description (as the AI agent sees it):**

> Returns how this MCP server is licensed, and — under metered licensing — how much has been consumed. Call this when the user asks about licensing, evaluation limitations, metered usage, remaining credit, or which product engine version is running. Returns a JSON object with `mode` ("evaluation", "licensed" or "metered"), `licensed` (true for both licensed and metered), `consumption` (null unless metered; otherwise `quantity` and `credit`, or `error` if the reading failed), and `server` / `engine` name and version. Takes no arguments and never modifies anything.

## Parameters

None.

## Example call

```json
{
  "name": "get_license_status",
  "arguments": {}
}
```

## Result

A JSON object describing the active licensing mode.

Evaluation mode — nothing configured:

```json
{
  "mode": "evaluation",
  "licensed": false,
  "server": { "name": "GroupDocs.Redaction.Mcp", "version": "26.9.0" },
  "engine": { "name": "GroupDocs.Redaction", "version": "26.6" },
  "note": "No license configured — output may carry evaluation limitations. ..."
}
```

The full `note` text names the variables to set: `GROUPDOCS_METERED_PUBLIC_KEY` and `GROUPDOCS_METERED_PRIVATE_KEY` for metered licensing, or `GROUPDOCS_LICENSE_PATH` for a license file.

Metered mode — both keys accepted:

```json
{
  "mode": "metered",
  "licensed": true,
  "source": "metered-keys",
  "consumption": { "quantity": 1234.5678, "credit": 9642.0 },
  "server": { "name": "GroupDocs.Redaction.Mcp", "version": "26.9.0" },
  "engine": { "name": "GroupDocs.Redaction", "version": "26.6" }
}
```

| Field | Meaning |
|---|---|
| `mode` | `evaluation`, `licensed`, or `metered` |
| `licensed` | `true` for both licensed and metered |
| `source` | `metered-keys` or `license-file`; absent in evaluation mode |
| `consumption.quantity` | Amount consumed — account-wide, `null` outside metered mode |
| `consumption.credit` | Credits consumed so far |
| `server` / `engine` | MCP server version and the underlying GroupDocs.Redaction engine version |
| `note` | Why licensing did not end up where you asked — present only when something needs attention |

**`"mode": "evaluation"` means your redactions are incomplete:** one document per process, one redaction, at most four replacements, trial badges on every page. A document redacted under those limits still contains the data it appears to have removed.

A rejected key pair does not fail silently: the mode reverts to `evaluation` and `note` carries the reason. See [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}}).

## Example prompts

* *"Is the redaction server licensed?"*
* *"How much metered credit have I used?"*
* *"Which GroupDocs.Redaction engine version is running?"*
