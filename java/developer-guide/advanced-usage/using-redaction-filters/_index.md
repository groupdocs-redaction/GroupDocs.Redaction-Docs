---
id: redaction-filters
url: redaction/java/redaction-filters
title: Using redaction filters
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---

GroupDocs.Redaction allows you to set the page-based scope for your redaction of two types:
*   page range, a given number of pages at certain offset from the beginning or the end of the page;
*   page area (on each page), which is a top-left based rectangle.  

All filters inherit from **RedactionFilter** and as an array are set to **Filters** property of the **ReplacementOptions**.

You can combine these filters in one set in order to set the scope of redaction to an area on a specific page. For more details, see [Use PDF redaction filters]({{< ref "redaction/java/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters" >}}) article.

## Redaction filters limitations

There are the following limitations of the redaction filters with GroupDocs.Redaction for Java v23.7:
*   Only PDF documents are not supported.  

We are working on adding more formats supported in future releases of GroupDocs.Redaction for Java.

## Learn more

You can find details and examples of using redaction filters with GroupDocs.Redaction for Java in one of these guides:
