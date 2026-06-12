---
id: redaction-filters
url: redaction/python-net/redaction-filters
title: Using redaction filters
linkTitle: Using redaction filters
weight: 1
description: "Scope a GroupDocs.Redaction for Python via .NET redaction to a page range or a rectangular page area using redaction filters, and combine them to target an area on specific pages."
keywords: redaction filters, page range filter, page area filter, scope redaction, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Redaction lets you set a page-based scope for a redaction, of two kinds:

- **Page range** — a number of pages at a given offset from the beginning or the end of the document;
- **Page area** — a top-left-based rectangle applied on each page.

All filters inherit from [RedactionFilter](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/redactionfilter/) and are passed as an array to the **filters** property of [ReplacementOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/replacementoptions/). Combine both kinds in one set to scope a redaction to an area on specific pages.

## Supported formats

Redaction filters apply to **PDF** documents. Support for additional formats is planned for future releases of GroupDocs.Redaction.

## In this section

- [Use PDF Redaction Filters]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters.md" >}}) — a runnable example that combines a page-range filter and a page-area filter to scope a redaction in a PDF.
