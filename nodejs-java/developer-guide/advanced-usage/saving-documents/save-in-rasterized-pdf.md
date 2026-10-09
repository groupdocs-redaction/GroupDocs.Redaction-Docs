---
id: save-in-rasterized-pdf
url: redaction/nodejs-java/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The following example demonstrates how to save the document as a rasterized PDF file:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor(Constants.SAMPLE_DOCX);
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
const tmp0 = new redaction.SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);
    // Saving as rasterized PDF with no suffix in file name
    redactor.save(tmp0);
}
finally {
  redactor.close();
}
```
