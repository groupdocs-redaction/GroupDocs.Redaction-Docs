---
id: redaction-filters
url: redaction/net/redaction-filters
title: Using redaction filters
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

GroupDocs.Redaction allows you to set the page-based scope for your redaction of two types:
*   page range, a given number of pages at certain offset from the beginning or the end of the page;
*   page area (on each page), which is a top-left based rectangle.  

All filters inherit from [RedactionFilter](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.redactions/redactionfilter/) and as an array are set to **Filters** property of the [ReplacementOptions](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.redactions/replacementoptions/).

You can combine these filters in one set in order to set the scope of redaction to an area on a specific page. For more details, see [Use PDF redaction filters]({{< ref "redaction/net/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters" >}}) article.

## Redaction filters limitations

There are the following limitations of the redaction filters with GroupDocs.Redaction v23.6:
*   Only PDF documents are not supported.  

We are working on adding more formats supported in future releases of GroupDocs.Redaction.

## Learn more

You can find details and examples of using redaction filters with GroupDocs.Redaction in one of these guides:
