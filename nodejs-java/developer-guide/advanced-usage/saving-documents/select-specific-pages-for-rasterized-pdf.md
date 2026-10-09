---
id: select-specific-pages-for-rasterized-pdf
url: redaction/nodejs-java/select-specific-pages-for-rasterized-pdf
title: Select specific pages for rasterized PDF
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Select specific pages for rasterized PDF

Saving document as a rasterized PDF, you can specify starting page index (zero based) and the number of pages from this index to save. Also, you can change the Compliance level from PDF/A-1b, which is used by default, to PDF/A-1a:



```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('MultipageSample.docx');
try 
{
const result = redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions(Color.RED)));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
const options = new redaction.SaveOptions();
        options.getRasterization().setEnabled(true);                           // the same as options.RasterizeToPDF = true;
        options.getRasterization().setPageIndex(5);                            // start from 6th page (index is 0-based)
        options.getRasterization().setPageCount(1);                            // save only one page
        options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);   // by default PdfComplianceLevel.Auto or PDF/A-1b
        options.setAddSuffix(true);
        redactor.save(options);
    }
}
finally {
  redactor.close();
}
```
