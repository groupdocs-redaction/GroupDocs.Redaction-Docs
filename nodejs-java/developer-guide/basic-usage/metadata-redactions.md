---
id: metadata-redactions
url: redaction/nodejs-java/metadata-redactions
title: Metadata redactions
weight: 6
description: "Erase or search/replace document metadata."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.EraseMetadataRedaction(redaction.MetadataFilters.All));
  redactor.apply(new redaction.MetadataSearchRedaction('.*@acme\\.com', '[email]'));
  redactor.save();
} finally {
  redactor.close();
}
```
