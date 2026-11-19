---
id: load-from-stream
url: redaction/nodejs-java/load-from-stream
title: Load from Stream
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Load from Stream

As an alternative to a local file, *Redactor* can open a document from stream.

The following example demonstrates how to load and redact a document using Stream:



{{< tabs "code-example-load-from-stream" >}}
{{< tab "load_from_stream.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const stream = new FileInputStream('sample.docx');
        try 
        {
const redactor = new redaction.Redactor(stream);
            try 
            {
                // Here we can use document instance to make redactions
                redactor.apply(new redaction.DeleteAnnotationRedaction());
                redactor.save();
            }
            finally {
  redactor.close();
}
        }
        finally {
  stream.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/loading-documents/load-from-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1.2 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/loading-documents/load-from-stream/CodeExampleLoadFromStream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
