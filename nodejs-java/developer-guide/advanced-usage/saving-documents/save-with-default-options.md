---
id: save-with-default-options
url: redaction/nodejs-java/save-with-default-options
title: Save with default options
weight: 5
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
  // Default: rasterize to PDF, add suffix
  redactor.save();
} finally {
  redactor.close();
}
```
