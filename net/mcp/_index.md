---
id: mcp-net
url: redaction/net/mcp
title: MCP server for .NET
linkTitle: MCP Server
weight: 7
description: "Install and configure the GroupDocs.Redaction MCP server for .NET — one-click install links for VS Code and Cursor, per-OS setup for Windows, Linux, and macOS, and the full environment-variable reference."
keywords: GroupDocs.Redaction MCP .NET, install MCP server dnx, MCP server Docker image, MCP server configuration, Model Context Protocol .NET
productName: GroupDocs.Redaction MCP Server for .NET
hideChildren: True
toc: True
---

Everything needed to **install and run** the GroupDocs.Redaction MCP server on the .NET platform. What the server *does* — its tools, use cases, and licensing model — is platform-independent and lives in the [MCP server section]({{< ref "redaction/mcp/_index.md" >}}).

| The .NET build at a glance | |
|---|---|
| Package | [`GroupDocs.Redaction.Mcp`](https://www.nuget.org/packages/GroupDocs.Redaction.Mcp) (current **26.9.0**) |
| One-command run | `dnx GroupDocs.Redaction.Mcp --yes` |
| Container images | `ghcr.io/groupdocs-redaction/redaction-net-mcp` · `groupdocs/redaction-net-mcp` |
| Prerequisites | [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) for the NuGet channel, or Docker |
| Source | [GroupDocs.Redaction.Mcp on GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp) |
| Release notes | [changelog](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp/tree/master/changelog) · [GitHub releases](https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp/releases) |

## Start here

1. **Install** for your operating system — [Windows]({{< ref "redaction/net/mcp/windows-installation.md" >}}) · [Linux]({{< ref "redaction/net/mcp/linux-installation.md" >}}) · [macOS]({{< ref "redaction/net/mcp/macos-installation.md" >}})
2. **Register it in your AI client** — [one-click links and per-client configs]({{< ref "redaction/net/mcp/install-in-ai-clients.md" >}})
3. **Point it at your documents** — [configuration]({{< ref "redaction/net/mcp/configuration.md" >}})
4. **License it** — evaluation, a license file, or metered keys: [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}})

## In this section

* [Install on Windows]({{< ref "redaction/net/mcp/windows-installation.md" >}})
* [Install on Linux]({{< ref "redaction/net/mcp/linux-installation.md" >}})
* [Install on macOS]({{< ref "redaction/net/mcp/macos-installation.md" >}})
* [Register in AI clients]({{< ref "redaction/net/mcp/install-in-ai-clients.md" >}}) — VS Code, Cursor, Claude, Visual Studio, Windsurf, Cline, Codex, Rider
* [Configuration]({{< ref "redaction/net/mcp/configuration.md" >}}) — storage, output, license, metered keys
* [System requirements]({{< ref "redaction/net/mcp/system-requirements.md" >}})
* [Troubleshooting (.NET)]({{< ref "redaction/net/mcp/troubleshooting.md" >}}) — `dnx`, native libraries, Docker daemon

## Platform-independent reference

* [Tools reference]({{< ref "redaction/mcp/tools-reference/_index.md" >}}) — `redact_text`, `redact_image_area`, `redact_annotations`, `erase_metadata`, `get_document_info`, `get_license_status`
* [Use cases]({{< ref "redaction/mcp/use-cases/_index.md" >}}) · [Supported formats]({{< ref "redaction/mcp/supported-formats.md" >}}) · [Troubleshooting & FAQ]({{< ref "redaction/mcp/troubleshooting-faq.md" >}})
