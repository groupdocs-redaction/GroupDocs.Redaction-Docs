---
id: use-page-area-redaction
url: redaction/nodejs-java/use-page-area-redaction
title: Use PageAreaRedaction
weight: 3
description: "Use PageAreaRedaction to redact text and images within a page range and page area."
keywords: PageAreaRedaction, page area, PDF, images
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

You can use **PageAreaRedaction** to redact an area of a specific page range from sensitive data in text, images, and annotations. Combine it with `PageRangeFilter` and `PageAreaFilter` on `ReplacementOptions`. This works for PDF and for other formats that support page filters (see [Supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}})). For embedded or standalone images, area coordinates follow the page (or visible) placement of the image.

The following example demonstrates how to apply **PageAreaRedaction** to the right half of the last page in a PDF document.

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const redactor = new redaction.Redactor('Sample.pdf');
        try 
        {
const rx = java.util.regex.Pattern.compile('urna');
const optionsText = new redaction.ReplacementOptions('[redarea]');
            optionsText.setFilters(new redaction.RedactionFilter[] {
                new redaction.PageRangeFilter(redaction.PageSeekOrigin.End, 0, 1), // last page
                new redaction.PageAreaFilter(new Point(300, 0), new Dimension(300, 840)) // right half of the page
            });
const optionsImg = new redaction.RegionReplacementOptions(Color.RED, new Dimension(100, 100));
const result = redactor.apply(new redaction.PageAreaRedaction(rx, optionsText, optionsImg));
            if (result.getStatus() !== redaction.RedactionStatus.Failed)
            {
                redactor.save();
            }                            
        }
        finally {
  redactor.close();
}
```

