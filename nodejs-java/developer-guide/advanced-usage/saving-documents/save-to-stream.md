---
id: save-to-stream
url: redaction/nodejs-java/save-to-stream
title: Save to stream
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
You might need to save a document to any custom file at any location on the local disc or a even a Stream.

The following example demonstrates how to save a document to any location.



```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const FileOutputStream = java.import('java.io.FileOutputStream');

const redactor = new redaction.Redactor('Sample.docx');
try {
  const result = redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions(Color.RED)));
  if (result.getStatus() !== redaction.RedactionStatus.Failed) {
    const fileStream = new FileOutputStream('C:\\Temp\\sample_output_file.pdf');
    try {
      const options = new redaction.RasterizationOptions();
      options.setEnabled(true);
      redactor.save(fileStream, options);
    } finally {
      fileStream.close();
    }
  }
} finally {
  redactor.close();
}
```
