---
id: load-from-stream
url: redaction/nodejs-java/load-from-stream
title: Load from stream
weight: 2
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const fs = require('fs');
const redaction = require('@groupdocs/groupdocs.redaction');

const stream = fs.createReadStream('sample.docx');
const redactor = new redaction.Redactor(stream);
try {
  redactor.apply(new redaction.DeleteAnnotationRedaction());
  redactor.save();
} finally {
  redactor.close();
}
```

When the stream has no file name, prefer [Load with file type]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/loading-documents/load-with-file-type.md" >}}).
