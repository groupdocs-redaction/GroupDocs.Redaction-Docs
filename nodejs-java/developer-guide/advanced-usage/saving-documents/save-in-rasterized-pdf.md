---
id: save-in-rasterized-pdf
url: redaction/nodejs-java/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));

  const options = new redaction.SaveOptions();
  options.setRasterizeToPDF(true);
  options.setAddSuffix(true);
  redactor.save(options);
} finally {
  redactor.close();
}
```
