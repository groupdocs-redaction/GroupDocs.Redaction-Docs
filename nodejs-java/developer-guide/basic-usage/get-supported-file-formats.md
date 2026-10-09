---
id: get-supported-file-formats
url: redaction/nodejs-java/get-supported-file-formats
title: Get supported file formats
weight: 1
description: This article shows that how to get the list of all supported file formats of GroupDocs.Redaction by using Java.
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Get supported file formats

GroupDocs.Redaction allows to get the list of all supported file formats by these steps:

*   Call *getSupportedFileTypes *of *FileType* class;
*   Enumerate through the collection of *FileType *objects*.*

The following example demonstrates how to get supported file formats list.



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const supportedFileTypes = redaction.FileType.getSupportedFileTypes();
const iterator = supportedFileTypes.iterator();      
while (iterator.hasNext())
{
const fileType = (FileType)iterator.next();
    console.log(fileType);
}
```
