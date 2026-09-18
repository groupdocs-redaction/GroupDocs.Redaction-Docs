---
id: mcp-troubleshooting-faq
url: redaction/mcp/troubleshooting-faq
title: Troubleshooting & FAQ
weight: 5
description: "Solutions to the most common GroupDocs.Redaction MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts."
keywords: MCP server not showing up in Claude Desktop, Claude can't see MCP tools, MCP server failed to start, dnx command not found, libgdiplus not found error, redact PDF with AI, remove sensitive data document MCP, black out text agent, GDPR redaction MCP
productName: GroupDocs.Redaction MCP Server
toc: True
---

Solutions to the most common GroupDocs.Redaction MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts.

{{< alert style="info" >}}
**Platform-specific troubleshooting:** runtime problems depend on which build you run. For the `dnx` runner, native graphics libraries, and the Docker channel, see [Troubleshooting (.NET)]({{< ref "redaction/net/mcp/troubleshooting.md" >}}). The issues on this page apply to every platform.
{{< /alert >}}

## Why is my MCP server not showing up in Claude Desktop?

1. **Restart the client** — every client reads its MCP config only at startup.
2. Check the config file location for your OS ([per-client reference]({{< ref "redaction/net/mcp/install-in-ai-clients.md" >}})) and that the entry sits under the right root key (`mcpServers` for Claude Desktop/Cursor/Windsurf, `servers` for VS Code/VS 2022).
3. Validate the JSON — a trailing comma silently breaks the whole file. If you used the [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer), a timestamped `.bak` of your previous config sits next to the file for comparison.

## The first tool call is slow or fails once, then works

A **cold cache**: on the very first use the server's package or image is still downloading while the client is already waiting on the connection. Warming it once fixes it for good — the exact command depends on your build: [.NET]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#the-first-tool-call-is-slow-or-fails-once-and-then-works).

## The server fails to start, or a runtime dependency is missing

These are properties of the build you run rather than of MCP, so the fixes live with the platform:

| Symptom | Where the fix is |
|---|---|
| `dnx: command not found` | [.NET troubleshooting]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#dnx-command-not-found) — `dnx` ships inside the .NET 10 SDK |
| `DllNotFoundException: libgdiplus` on Linux/macOS | [.NET troubleshooting]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#dllnotfoundexception-libgdiplus) — install the native graphics libraries, or use the Docker image |
| "docker daemon not reachable" | [.NET troubleshooting]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#docker-daemon-not-reachable) — start Docker Desktop or `dockerd` |

## The agent says a file does not exist

Pass the **file name**, not a full path from your machine: the server resolves names inside its configured storage folder. When a name is not found the tool responds with the list of files it can see, so the agent can correct itself — check that list against [`GROUPDOCS_MCP_STORAGE_PATH`]({{< ref "redaction/net/mcp/configuration.md" >}}).

## Is the redacted text really gone?

For [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}), yes — the matching text is replaced in the document rather than covered over, which is the difference between redaction and drawing a black rectangle in a viewer. But "really gone" is a claim about the **whole file**, so finish the job: text can also live in annotations, in metadata, and in images of the page. That is why this server has four redaction tools rather than one.

## Does it find sensitive data for me?

No. You (or the agent) supply the **pattern**. The tools apply it exactly and predictably — there is no classifier guessing at what looks like a national ID. That is a deliberate boundary: an agent proposing patterns is useful; an agent silently deciding what counts as sensitive is not something to trust with a legal disclosure.

## What about text inside images?

[`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) works on the text layer. A name that appears in a scanned page is part of an image, and must be covered with [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) using coordinates. There is no OCR step in this server.

## How do I verify a redaction?

Read the redacted copy back and search it: run the same pattern again and expect zero matches, check the metadata with [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) applied, and look at the pages. The [verification workflow]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}) sets this out step by step. Do not skip it — a redaction you have not verified is a claim, not a control.

## Why does only part of my document get redacted?

Almost certainly **evaluation mode**: one redaction per document, capped at four replacements. A pattern matching twelve times leaves eight in place, and nothing in the response says so. [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) first, every time.

## Verifying an installation end-to-end

Ask your agent *"list your GroupDocs redaction tools and the license status"* — it should name `redact_text`, `redact_image_area`, `redact_annotations`, `erase_metadata`, `get_document_info`, `get_license_status`. For a scripted check that performs the real MCP handshake and a live call through the engine, see [verifying a .NET installation]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end).

## Still stuck?

Post your config (redact license paths) and the client name in the [Redaction forum](https://forum.groupdocs.com/c/redaction/33) — we answer MCP questions daily. Bugs: [GitHub issues](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp/issues).
