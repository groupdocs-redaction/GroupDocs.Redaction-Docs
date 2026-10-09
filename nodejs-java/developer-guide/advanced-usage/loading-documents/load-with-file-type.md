---
id: load-with-file-type
url: redaction/nodejs-java/load-with-file-type
title: Load with file type
weight: 6
description: "Pass an explicit FileType in LoadOptions when opening a stream or mismatched extension."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
When opening from a stream without a file name, or when the extension does not match the real format, set `FileType` on `LoadOptions`. Detection is skipped and the specified type is used. Default is `FileType.getUnknown()`.

```js
const fs = require('fs');
const redaction = require('@groupdocs/groupdocs.redaction');

const stream = fs.createReadStream('sample.docx');
const redactor = new redaction.Redactor(
  stream,
  new redaction.LoadOptions(redaction.FileType.getDOCX()));
try {
  redactor.apply(new redaction.DeleteAnnotationRedaction());
  redactor.save();
} finally {
  redactor.close();
}

const redactor2 = new redaction.Redactor(
  'LoremIpsum.pdf',
  new redaction.LoadOptions(redaction.FileType.getPDF()));
try {
  redactor2.apply(new redaction.ExactPhraseRedaction(
    'Lorem',
    new redaction.ReplacementOptions('[x]')));
  redactor2.save();
} finally {
  redactor2.close();
}
```
