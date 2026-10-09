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
