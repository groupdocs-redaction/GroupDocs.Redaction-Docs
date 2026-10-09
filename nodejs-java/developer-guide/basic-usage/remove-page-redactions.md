---
id: remove-page-redactions
url: redaction/nodejs-java/remove-page-redactions
title: Remove page redactions
weight: 10
description: "Remove a range of pages, slides, or worksheets."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.pdf');
try {
  redactor.apply(new redaction.RemovePageRedaction(
    redaction.PageSeekOrigin.Begin,
    0,
    1));
  redactor.save();
} finally {
  redactor.close();
}
```
