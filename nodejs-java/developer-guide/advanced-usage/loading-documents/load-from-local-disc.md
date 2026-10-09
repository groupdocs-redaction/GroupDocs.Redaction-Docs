---
id: load-from-local-disc
url: redaction/nodejs-java/load-from-local-disc
title: Load from local disc
weight: 1
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.DeleteAnnotationRedaction());
  redactor.save();
} finally {
  redactor.close();
}
```
