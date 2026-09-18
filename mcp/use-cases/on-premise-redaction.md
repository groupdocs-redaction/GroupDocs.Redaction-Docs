---
id: mcp-uc-on-premise-redaction
url: redaction/mcp/use-cases/on-premise-redaction
title: "Running GroupDocs MCP servers on-premise: architecture and security model"
linkTitle: On-premise deployment
weight: 5
description: "Run document redaction for AI agents fully on-premise: local stdio transport, no external endpoints, no telemetry, and an honest account of what travels in the conversation."
keywords: on-premise MCP server, air-gapped redaction, MCP security model, local document redaction AI, no cloud redaction
productName: GroupDocs.Redaction MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "Running GroupDocs MCP servers on-premise: architecture and security model"
        description: "Run document redaction for AI agents fully on-premise: local stdio transport, no external endpoints, no telemetry, and an honest account of what travels in the conversation."
        steps:
        - name: "Run the pinned image inside the perimeter"
          text: "Start the GroupDocs.Redaction MCP server from its versioned Docker image as a child process of the AI client."
        - name: "Mount only the folders the agent may reach"
          text: "Map the document folder read-write and the license folder read-only."
        - name: "Choose the license mode"
          text: "Use a license file for fully offline operation; metered licensing needs outbound egress for usage reports."
---

Run redaction for AI agents **fully on-premise**: the GroupDocs.Redaction MCP server uses local stdio transport with **no external endpoints, no inbound ports, and no telemetry**. For this product that is the baseline requirement — the documents being redacted are the ones that cannot be sent anywhere. This page is the one to send your security reviewer.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "redaction/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The architecture in one picture

```text
+--------------+          +--------------------+         +------------------+
|  AI client   |  stdio   | MCP server process | reads / | local filesystem |
| (Claude, VS  | <----->  | (GroupDocs engine) | <-----> | storage / output |
| Code, agent) | JSON-RPC |   child process    |  writes |     folders      |
+--------------+          +--------------------+         +------------------+
```

* **Transport:** the AI client *starts the server as a child process* and communicates over standard input/output. The server never listens on a network socket.
* **Data path:** agent → local server → local filesystem. Documents and redacted copies are read and written in the folders you configure; no document content is transmitted anywhere.
* **Network use:** only at install time (nuget.org or ghcr.io/docker.io). At runtime the server makes no outbound calls. Air-gapped: pre-pull the image or pre-cache the package and pin the version.
* **Telemetry:** none. The engine processes documents in-process.

## The part that deserves care

The documents stay local. **The conversation does not.**

With a cloud-hosted model, everything the agent says travels to the model provider — and in redaction work that can include the very strings you are removing. *"I redacted 14 occurrences of jane.smith@example.com"* has just sent the address you were protecting. So has *"the pattern matched the client name Acme Holdings"*.

Three ways to handle it, in order of strength:

1. **Run a local model.** Nothing leaves the perimeter at all.
2. **Ask for counts, not values.** *"Report how many matches, not what they were"* is a prompt the agent will follow.
3. **Pass patterns by description** where possible — *"our standard account-number pattern"* rather than a literal customer identifier.

None of this is a limitation of the server; it is a property of using a hosted model. It is better stated plainly than discovered later.

## Docker deployment inside the perimeter

```bash
docker run --rm -i \
  -v /srv/case-files:/data \
  -v /srv/licenses:/license:ro \
  -e GROUPDOCS_MCP_STORAGE_PATH=/data \
  -e GROUPDOCS_MCP_OUTPUT_PATH=/data/redacted \
  -e GROUPDOCS_LICENSE_PATH=/license/GroupDocs.Redaction.lic \
  ghcr.io/groupdocs-redaction/redaction-net-mcp:26.9.0
```

* Pin the tag (`:26.9.0`, not `:latest`).
* A separate output path keeps redacted copies away from the originals — worth doing here more than anywhere.
* Licence read-only; mount only the folders the agent should reach.

## License management

* **License file** — read from local disk by the local process. Fully offline, and the only way to get complete redactions.
* **Metered (pay-per-use)** — reports *usage* to GroupDocs servers, so it needs outbound egress. Document content is never part of that report.

Both are covered in [Licensing]({{< ref "redaction/mcp/getting-started/licensing.md" >}}).

## What this fits — honestly

**A good fit:** disclosure and FOI preparation, GDPR data-subject requests, internal sanitisation before sharing, and any environment where documents cannot leave the network for processing.

**Not what this is:** a compliance guarantee. The server removes what you tell it to remove, in the file you give it. Whether your patterns were complete, whether the right file was released, and whether the result satisfies a particular regulation are decisions that stay with you — which is why [verification]({{< ref "redaction/mcp/use-cases/verify-a-redaction.md" >}}) is a documented step rather than an optional extra.

## FAQ

**Does any document content leave the machine?** Not from the server. What the agent reports back does travel to your model provider — see above.

**Does it need internet at runtime?** No — only at install, and when metered licensing is enabled.

**Can I run it air-gapped?** Yes, and for this product it is the recommended shape: pre-pull the image, use a license file, pin the version.

**What ports does it open?** None. stdio only.

**How do I prove that?** The [verification script]({{< ref "redaction/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end) performs a real handshake and a real engine call so you can watch exactly what happens.
