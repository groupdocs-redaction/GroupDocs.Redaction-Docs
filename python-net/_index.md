---
id: home
url: redaction/python-net
title: GroupDocs.Redaction for Python via .NET
weight: 1
description: "Native Python library that permanently redacts sensitive content — text, metadata, annotations, and image areas — from PDF, Word, Excel, PowerPoint, and image files on Windows, Linux, and macOS. No Microsoft Office or Adobe Acrobat required."
keywords: GroupDocs.Redaction, Python via .NET, document redaction, redact PDF, redact DOCX, redact XLSX, metadata removal, annotation redaction, image redaction, PII removal, rasterized PDF, on-premise, Windows, Linux, macOS
productName: GroupDocs.Redaction for Python via .NET
hideChildren: true
toc: True
structuredData:
    showOrganization: true
---

<img src="/logo/128x128/groupdocs-redaction-python.png" alt="groupdocs-redaction-python-home" align="left" style="width:110px; margin: 0 30px 30px 0"/>

<img src="https://img.shields.io/pypi/v/groupdocs-redaction-net?label=GroupDocs.Redaction%20PyPI" alt="PyPI package">
<img src="https://img.shields.io/pypi/dm/groupdocs-redaction-net?label=pypi%20downloads" alt="PyPI downloads">

{{< button style="primary" link="https://releases.groupdocs.com/redaction/python-net/release-notes/" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#document"></use></svg> Release notes {{< /button >}}
{{< button style="primary" link="https://pypi.org/project/groupdocs-redaction-net/" >}} {{< icon "gdoc_download" >}} Download from PyPI {{< /button >}}
{{< button style="primary" link="https://products.groupdocs.app/redaction/family" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#app"></use></svg> Online app {{< /button >}}

[GroupDocs.Redaction for Python via .NET](https://products.groupdocs.com/redaction/python-net/) is a document redaction API that permanently removes sensitive or classified content from documents across many formats. It provides a unified, format-independent interface to redact text by exact phrase or regular expression, scrub or rewrite metadata, black out image areas, rewrite or delete annotations, and remove pages — then save the result in its original format or as a rasterized PDF so redacted content cannot be recovered.

<div style="clear:left"></div>

## Quick example

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

# Redact every occurrence of "John Doe" in a document
with Redactor("sample.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("John Doe", ReplacementOptions("[personal]")))
    redactor.save()
```

## Features

- **Text Redaction**: Replace or hide text matched by an exact phrase (case-sensitive or RTL-aware) or a regular expression, with a replacement string or a colored box.
- **Metadata Redaction**: Erase or rewrite document metadata, wholesale or filtered by property.
- **Image & Annotation Redaction**: Black out image areas, clean embedded image metadata, and rewrite or delete annotations.
- **Page Removal & Rasterization**: Remove pages or page ranges, and optionally flatten the result to a rasterized PDF (with PDF/A compliance) so redacted content is unrecoverable.
- **Redaction Policies**: Describe a reusable set of redactions as a policy and apply it across many documents.

## Supported File Formats

GroupDocs.Redaction supports a wide range of file formats. For a complete list, see the [full list of supported formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}).

- **Microsoft Office** (Word, Excel, PowerPoint)
- **PDF** (Standard PDFs, PDF/A output)
- **OpenDocument** (ODT, ODS, ODP)
- **Images** (JPEG, PNG, GIF, BMP, TIFF)
- **Text** (TXT, RTF, CSV)

## Getting Started

To get started, refer to the [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}), [Supported File Formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}), [Installation]({{< ref "redaction/python-net/getting-started/installation.md" >}}), and [Hello, World!]({{< ref "redaction/python-net/getting-started/hello-world.md" >}}) sections for setup instructions and your first redaction.

## Developer Guide

For practical, runnable code examples covering basic and advanced redaction, see the [Developer Guide]({{< ref "redaction/python-net/developer-guide/_index.md" >}}) section. It walks through loading documents, applying text, metadata, image, annotation, and page redactions, saving and rasterizing results, and building reusable redaction policies.

## AI Agents & LLM Integration

Using an AI coding assistant? The [AI Agents & LLM Integration]({{< ref "redaction/python-net/agents-and-llm-integration.md" >}}) page covers the bundled `AGENTS.md` reference, the GroupDocs MCP server, and machine-readable documentation.

## Technical Support

If you experience any issues or have suggestions, see [Technical Support]({{< ref "redaction/python-net/technical-support.md" >}}) for the available channels — the free support forum and the paid helpdesk. For licensing and evaluation questions, see [Licensing and Subscription]({{< ref "redaction/python-net/getting-started/licensing-and-subscription.md" >}}).
