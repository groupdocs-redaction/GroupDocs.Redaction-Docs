---
id: pre-rasterize
url: redaction/nodejs-java/pre-rasterize
title: Pre-rasterize
weight: 5
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
Force rasterization on load when the source format must be processed as a PDF of page images:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const loadOptions = new redaction.LoadOptions(true); // preRasterize
const redactor = new redaction.Redactor('sample.docx', loadOptions);
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```
