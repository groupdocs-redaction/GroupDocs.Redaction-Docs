---
id: use-pdf-redaction-filters
url: redaction/nodejs-java/use-pdf-redaction-filters
title: Use PDF redaction filters
weight: 2
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const Point = java.import('java.awt.Point');
const Dimension = java.import('java.awt.Dimension');

const redactor = new redaction.Redactor('sample.pdf');
try {
  const options = new redaction.ReplacementOptions('[redacted]');
  options.setFilters([
    new redaction.PageRangeFilter(redaction.PageSeekOrigin.Begin, 0, 1),
    new redaction.PageAreaFilter(new Point(0, 0), new Dimension(300, 100))
  ]);

  redactor.apply(new redaction.ExactPhraseRedaction('sensitive', options));
  redactor.save();
} finally {
  redactor.close();
}
```
