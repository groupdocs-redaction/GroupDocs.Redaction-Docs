---
id: redaction-filters
url: redaction/nodejs-java/redaction-filters
title: Using redaction filters
weight: 1
description: "Limit redactions by page range or page area for PDF, presentations, and images."
keywords: PageRangeFilter, PageAreaFilter, redaction filters
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---

GroupDocs.Redaction allows you to set the page-based scope for your redaction of two types:
*   page range, a given number of pages at certain offset from the beginning or the end of the document;
*   page area (on each page), which is a top-left based rectangle.

All filters inherit from **RedactionFilter** and as an array are set to **Filters** property of the **ReplacementOptions**.

You can combine these filters in one set in order to set the scope of redaction to an area on a specific page. For more details, see [Use PDF redaction filters]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters" >}}) and [Use PageAreaRedaction]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/use-page-area-redaction" >}}).

## Supported formats

Page filters apply to formats that expose page (or slide) layout and image placement, including:

* PDF
* Presentations (PPTX and related)
* Raster images (when using area / OCR redactions with page filters)

For formats listed with **Page Filters** in [Supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}), coordinates are based on the page (or visible image) size. Embedded images that differ in pixel size from their on-page shape are redacted using page placement.

## Learn more

You can find details and examples of using redaction filters with GroupDocs.Redaction for Node.js via Java in one of these guides:
