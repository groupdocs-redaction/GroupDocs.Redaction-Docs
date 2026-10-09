---
id: get-supported-file-formats
url: redaction/nodejs-java/get-supported-file-formats
title: Get supported file formats
weight: 12
description: "List file types supported by GroupDocs.Redaction."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const formats = redaction.FileType.getSupportedFileTypes();
for (let i = 0; i < formats.size(); i++) {
  console.log(formats.get(i).toString());
}
```

Also see [Supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}).
