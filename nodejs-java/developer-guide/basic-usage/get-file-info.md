---
id: get-file-info
url: redaction/nodejs-java/get-file-info
title: Get file info
weight: 11
description: "Read basic document information before redaction."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  const info = redactor.getDocumentInfo();
  console.log('Pages:', info.getPageCount());
  console.log('File type:', info.getFileType());
} finally {
  redactor.close();
}
```
