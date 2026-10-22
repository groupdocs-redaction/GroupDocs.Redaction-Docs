# AGENTS.md

Guidance for AI agents (and people) working in this documentation repository.

## What this is

Markdown sources for the GroupDocs.Redaction documentation site:

https://docs.groupdocs.com/redaction/

The Java section is:

https://docs.groupdocs.com/redaction/java/

This tree also contains `net/`, `nodejs-java/`, `python-net/`, and `mcp/`. Do not delete those folders. Do not treat `mcp/` as the Java SDK.

## Java package

- groupId: `com.groupdocs`
- artifactId: `groupdocs-redaction`
- Repository: https://releases.groupdocs.com/java/repo/
- Installation topic: `java/getting-started/installation.md` (it states the version it documents and links the releases repository)

## Useful paths

- `java/_index.md` - Java section home
- `java/getting-started/installation.md` - Maven, Gradle, and other build tools
- `java/getting-started/supported-document-formats.md` - format matrix
- `java/getting-started/sdk-cloud-mcp.md` - when to use the Java SDK, Cloud, or MCP

## Build

See `README.md`, `build_docs.cmd`, and `build_docs.sh`. This repository is Hugo source, not a library to import.

## Do not

- Invent a format count. Use the Java format matrix.
- Edit Cloud product repositories from this tree.
- Patch the MCP server repository. MCP is link-only: https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp
