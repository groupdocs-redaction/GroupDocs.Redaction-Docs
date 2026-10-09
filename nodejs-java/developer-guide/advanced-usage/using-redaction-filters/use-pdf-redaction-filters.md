---
id: use-pdf-redaction-filters
url: redaction/nodejs-java/use-pdf-redaction-filters
title: Use PDF redaction filters
weight: 2
description: "Set page-level scope for redactions using PageRangeFilter and PageAreaFilter."
keywords: PageRangeFilter, PageAreaFilter, PDF page scope
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

You can combine **PageRangeFilter** and **PageAreaFilter** in one set to limit a redaction to an area on a specific page (or slide). Assign the filters array to the **Filters** property of **ReplacementOptions**. The same approach applies to PDF and to other formats that support page filters.

The following example demonstrates how to apply redaction to the bottom half of the last page in a PDF document.

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const redactor = new redaction.Redactor('Sample.pdf');
        try 
        {
            // Get the actual size information for the last page:
const info = redactor.getDocumentInfo();
const lastPage = info.getPages().get(info.getPageCount() - 1);
const options = new redaction.ReplacementOptions('[secret]');
            options.setFilters(new redaction.RedactionFilter[] {
                new redaction.PageRangeFilter(redaction.PageSeekOrigin.End, 0, 1),
                new redaction.PageAreaFilter(new Point(0, lastPage.getHeight()/2),
                    new Dimension(lastPage.getWidth(), lastPage.getHeight()/2))
            });
const result = redactor.apply(new redaction.ExactPhraseRedaction('bibliography', false, options));
            if (result.getStatus() !== redaction.RedactionStatus.Failed)
            {
                redactor.save();
            }                            
        }
        finally {
  redactor.close();
}
```

