---
id: use-page-area-redaction
url: redaction/nodejs-java/use-page-area-redaction
title: Use PageAreaRedaction
weight: 3
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
`PageAreaRedaction` redacts text (and optionally image areas) within a page scope defined by filters.

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const Point = java.import('java.awt.Point');
const Dimension = java.import('java.awt.Dimension');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('sample.pdf');
try {
  const optionsText = new redaction.ReplacementOptions('[redarea]');
  optionsText.setFilters([
    new redaction.PageRangeFilter(redaction.PageSeekOrigin.End, 0, 1),
    new redaction.PageAreaFilter(new Point(300, 0), new Dimension(300, 840))
  ]);

  const optionsImg = new redaction.RegionReplacementOptions(
    Color.RED,
    new Dimension(100, 100));

  redactor.apply(new redaction.PageAreaRedaction(
    java.import('java.util.regex.Pattern').compile('urna'),
    optionsText,
    optionsImg));
  redactor.save();
} finally {
  redactor.close();
}
```
