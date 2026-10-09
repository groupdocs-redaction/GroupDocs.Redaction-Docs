---
id: use-redaction-policies
url: redaction/nodejs-java/use-redaction-policies
title: Use redaction policies
weight: 4
description: "Load and apply a redaction policy XML to one or more documents."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const policy = redaction.RedactionPolicy.load('RedactionPolicy.xml');
const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(policy);
  redactor.save();
} finally {
  redactor.close();
}
```
