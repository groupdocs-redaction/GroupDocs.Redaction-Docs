---
id: load-from-local-disc
url: redaction/nodejs-java/load-from-local-disc
title: Load from local disc
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Load from local disc

*GroupDocs.Redaction.Redactor* class is a main class in Redaction API, providing functionality to open a document. When document is located on the local disk, you can pass its path to *Redactor *class constructor.

The following example demonstrates how to open a document from local disc:



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try 
{
    // Here we can use document instance to perform redactions   
    redactor.apply(new redaction.DeleteAnnotationRedaction());
    redactor.save();
}
finally {
  redactor.close();
}
```
