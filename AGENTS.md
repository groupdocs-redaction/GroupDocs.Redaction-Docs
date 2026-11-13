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

## Python package

- PyPI: `groupdocs-redaction-net` (https://pypi.org/project/groupdocs-redaction-net/); pip also installs `groupdocs-shared-net`, which holds `groupdocs.pydrawing` and `groupdocs.pycore`
- Section: https://docs.groupdocs.com/redaction/python-net/
- Installation topic: `python-net/getting-started/installation.md` (wheel names, the offline install of both wheels, the Linux packages)
- Agent guide: `python-net/agents-and-llm-integration.md` embeds the `AGENTS.md` that ships inside the wheel
- `python-net/_sample_files/` comes from GroupDocs.Redaction-SampleFiles (`tools/sync.ps1`) and `python-net/_output_files/` from docs-to-code-examples (`generate_outputs.py`); do not edit either by hand

## Useful paths

- `java/_index.md` - Java section home
- `java/getting-started/installation.md` - Maven, Gradle, and other build tools
- `java/getting-started/supported-document-formats.md` - format matrix
- `java/getting-started/sdk-cloud-mcp.md` - when to use the Java SDK, Cloud, or MCP
- `python-net/_index.md` - Python section home
- `python-net/getting-started/installation.md` - pip, wheels and platform packages
- `python-net/getting-started/supported-document-formats.md` - Python format matrix, measured per release

## Build

See `README.md`, `build_docs.cmd`, and `build_docs.sh`. This repository is Hugo source, not a library to import.

## Do not

- Invent a format count. Use the Java format matrix for Java and the Python one for Python.
- Edit Cloud product repositories from this tree.
- Patch the MCP server repository. MCP is link-only: https://github.com/groupdocs-redaction/GroupDocs.Redaction.Mcp
