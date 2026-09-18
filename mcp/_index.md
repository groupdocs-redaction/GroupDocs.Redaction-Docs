---
id: mcp
url: redaction/mcp
title: GroupDocs.Redaction MCP Server
weight: 6
description: "GroupDocs.Redaction MCP server lets AI agents like Claude, Cursor, and Copilot redact text, image areas, annotations, and metadata from documents — locally, with nothing uploaded."
keywords: document redaction MCP server, redact PDF with AI agent, remove sensitive data MCP, GDPR redaction AI, Claude redact documents locally
productName: GroupDocs.Redaction MCP Server
hideChildren: True
toc: True
---

**GroupDocs.Redaction MCP server** lets AI agents like Claude, Cursor, and Copilot **redact documents** — text by pattern, areas of a page, annotations, and metadata — **locally on your machine**. For a redaction tool that property is not a feature, it is the requirement: the documents you redact are the ones that must not be uploaded anywhere. 

Run it with one command. The Docker image is self-contained — the runtime and every native dependency the engine needs are inside it:

```bash
docker run --rm -i -v $(pwd)/documents:/data \
  ghcr.io/groupdocs-redaction/redaction-net-mcp:latest
```

With the .NET 10 SDK installed, the same server also runs without Docker:

```bash
dnx GroupDocs.Redaction.Mcp --yes
```

Both are the **.NET** build of the server and run on Windows, Linux, and macOS. Other platforms will each get their own launcher — see [Install for your platform](#install-for-your-platform).

Or use the [guided installer]({{< ref "redaction/mcp/getting-started/_index.md" >}}) to register the server in your AI client, verify the setup, and configure shared folders in one pass.

{{< alert style="warning" >}}
**Evaluation mode produces incomplete redactions.** One document per process, one redaction, capped at **four replacements**, plus trial badges — and nothing in the response says a match was skipped. A document redacted unlicensed can look clean and still contain the data. Check [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) before every run that matters; see [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}}).
{{< /alert >}}

## What you can do

Sensitive data hides in four places, and there is a tool for each (full details in the [tools reference]({{< ref "redaction/mcp/tools-reference/_index.md" >}})):

| Where the data is | Tool |
|---|---|
| In the text | [`redact_text`]({{< ref "redaction/mcp/tools-reference/redact-text.md" >}}) — regular-expression matching, replaced in the document |
| In an image or scan | [`redact_image_area`]({{< ref "redaction/mcp/tools-reference/redact-image-area.md" >}}) — a solid box over a rectangle |
| In comments and notes | [`redact_annotations`]({{< ref "redaction/mcp/tools-reference/redact-annotations.md" >}}) — replace or delete annotations |
| In the file's properties | [`erase_metadata`]({{< ref "redaction/mcp/tools-reference/erase-metadata.md" >}}) — author, company, dates, keywords |

Plus [`get_document_info`]({{< ref "redaction/mcp/tools-reference/get-document-info.md" >}}) for page dimensions and [`get_license_status`]({{< ref "redaction/mcp/tools-reference/get-license-status.md" >}}) for the check above.

A complete pass uses all four. Cleaning the body text and shipping a file whose margin comments and author field still name the person is the most common way redactions fail.

## Install for your platform

Installation, prerequisites, and client configuration are platform-specific; the tools and licensing model below are the same everywhere.

| Platform | Status | Install and setup |
|---|---|---|
| .NET | **Available** | [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}) |
| Java | Planned | [Tell us you need it](https://forum.groupdocs.com/c/redaction/33) |
| Python | Planned | [Tell us you need it](https://forum.groupdocs.com/c/redaction/33) |
| Node.js | Planned | [Tell us you need it](https://forum.groupdocs.com/c/redaction/33) |

## What the agent does, and what it does not

The agent **proposes patterns** and drives the calls; the engine **applies them exactly**. There is no classifier deciding what looks sensitive — you get predictable, reviewable behaviour, and the responsibility for what counts as sensitive stays with you.

That division is deliberate. An agent that quietly decided which names to remove would be impossible to audit, and a redaction you cannot audit is not a control. Ask the agent to report **match counts** and to verify afterwards — [how to verify]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}).

## Supported AI clients

| Client | How it connects |
|---|---|
| Claude Desktop | `claude_desktop_config.json` |
| Claude Code | `claude mcp add` CLI |
| VS Code / GitHub Copilot | user-level or workspace `mcp.json` |
| Visual Studio 2022 (17.14+) | `.mcp.json` in the solution root |
| Cursor | `~/.cursor/mcp.json` |
| Windsurf | `~/.codeium/windsurf/mcp_config.json` |
| Cline | Cline MCP settings |
| Codex CLI | `codex mcp add` CLI |
| JetBrains Rider | manual registration (Settings → AI Assistant → MCP) |

Exact config blocks for every client: [Register in AI clients]({{< ref "redaction/net/mcp/install-in-ai-clients.md" >}}).

## Delivery channels

| | Docker (recommended) | NuGet (`dnx`) |
|---|---|---|
| Prerequisites | Docker only | .NET 10 SDK (+ `libgdiplus` on Linux/macOS) |
| Native dependencies | bundled in the image | installed by you (or the setup script) |
| Package | `ghcr.io/groupdocs-redaction/redaction-net-mcp` | `GroupDocs.Redaction.Mcp` on NuGet |
| Architectures | linux/amd64 + linux/arm64 (Apple Silicon native) | any OS with .NET 10 |

## How it works

The server uses MCP's **local stdio transport**: your AI client starts the server as a child process and talks to it over standard input/output. No inbound ports, no external endpoints, no telemetry — the data path is *agent → local server → local filesystem*. Details, including what still reaches your model provider: [On-premise architecture]({{< ref "redaction/mcp/use-cases/on-premise-redaction.md" >}}).

## When you need more than a black rectangle

Drawing a box in a PDF viewer leaves the text underneath, and everyone has seen a "redacted" document that could be copy-pasted. Choose this server when you need: text **replaced in the document**, not covered; the same model across 30+ formats; annotations and metadata handled as part of the same pass; pattern-based work an agent can drive over many files; and the fidelity of the commercial GroupDocs engine trusted by enterprise teams for over a decade.

## Resources

* [Quick start]({{< ref "redaction/mcp/getting-started/_index.md" >}}) · [Use cases]({{< ref "redaction/mcp/use-cases/_index.md" >}}) · [Troubleshooting & FAQ]({{< ref "redaction/mcp/troubleshooting-faq.md" >}})
* GitHub: [server source](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp) · [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer) · [integration tests](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp.Tests)
* [NuGet package](https://www.nuget.org/packages/GroupDocs.Redaction.Mcp) · [Docker image](https://github.com/orgs/groupdocs-redaction/packages/container/package/redaction-net-mcp) · [MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=io.github.groupdocs-redaction/groupdocs-redaction-mcp)
* Questions: [Redaction forum](https://forum.groupdocs.com/c/redaction/33)
