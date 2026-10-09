---
id: save-to-stream
url: redaction/nodejs-java/save-to-stream
title: Save to stream
weight: 4
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const fs = require('fs');
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));

  const out = fs.createWriteStream('result.pdf');
  const raster = new redaction.RasterizationOptions();
  raster.setEnabled(true);
  redactor.save(out, raster);
} finally {
  redactor.close();
}
```
