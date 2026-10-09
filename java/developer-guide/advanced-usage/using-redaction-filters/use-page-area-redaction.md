---
id: use-page-area-redaction
url: redaction/java/use-page-area-redaction
title: Use PageAreaRedaction
weight: 3
description: "Use PageAreaRedaction to redact text and images within a page range and page area."
keywords: PageAreaRedaction, page area, PDF, images
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---

You can use **PageAreaRedaction** to redact an area of a specific page range from sensitive data in text, images, and annotations. Combine it with `PageRangeFilter` and `PageAreaFilter` on `ReplacementOptions`. This works for PDF and for other formats that support page filters (see [Supported document formats]({{< ref "redaction/java/getting-started/supported-document-formats.md" >}})). For embedded or standalone images, area coordinates follow the page (or visible) placement of the image.

The following example demonstrates how to apply **PageAreaRedaction** to the right half of the last page in a PDF document.

```java
        final Redactor redactor = new Redactor("Sample.pdf");
        try 
        {
            java.util.regex.Pattern rx = java.util.regex.Pattern.compile("urna");
            ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
            optionsText.setFilters(new RedactionFilter[] {
                new PageRangeFilter(PageSeekOrigin.End, 0, 1), // last page
                new PageAreaFilter(new java.awt.Point(300, 0), new java.awt.Dimension(300, 840)) // right half of the page
            });
            RegionReplacementOptions optionsImg = new RegionReplacementOptions(java.awt.Color.RED, new java.awt.Dimension(100, 100));
            RedactorChangeLog result = redactor.apply(new PageAreaRedaction(rx, optionsText, optionsImg));
            if (result.getStatus() != RedactionStatus.Failed)
            {
                redactor.save();
            }                            
        }
        finally { redactor.close(); }
```

