---
id: save-in-original-format
url: redaction/nodejs-java/save-in-original-format
title: Save in original format
weight: 1
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
  options.setAddSuffix(true);
  options.setRasterizeToPDF(false);
  options.setRedactedFileSuffix('Redacted');
  redactor.save(options);
} finally {
  redactor.close();
}
```
