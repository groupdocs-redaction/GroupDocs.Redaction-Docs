---
id: spreadsheet-redactions
url: redaction/nodejs-java/spreadsheet-redactions
title: Spreadsheet redactions
weight: 9
description: "Redact spreadsheet cells, including column-scoped text redaction."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.xlsx');
try {
  const filter = new redaction.CellFilter();
  filter.setColumnIndex(1);
  filter.setWorkSheetIndex(0);

  redactor.apply(new redaction.CellColumnRedaction(
    filter,
    '\\d{2,}',
    new redaction.ReplacementOptions('[redacted]')));
  redactor.save();
} finally {
  redactor.close();
}
```
