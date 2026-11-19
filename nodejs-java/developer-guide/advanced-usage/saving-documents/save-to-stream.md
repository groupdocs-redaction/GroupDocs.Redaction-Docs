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



{{< tabs "code-example-save-to-stream" >}}
{{< tab "save_to_stream.js" >}}
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
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/save-to-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1003 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/save-to-stream/CodeExampleSaveToStream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
