---
id: annotation-redactions
url: redaction/nodejs-java/annotation-redactions
title: Annotation redactions
weight: 7
description: "Rewrite or delete annotations and comments."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.pdf');
try {
  redactor.apply(new redaction.AnnotationRedaction('(?i)approved', '[review]'));
  redactor.apply(new redaction.DeleteAnnotationRedaction('(?i)internal'));
  redactor.save();
} finally {
  redactor.close();
}
```
