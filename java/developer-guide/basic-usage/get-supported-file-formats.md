---
id: get-supported-file-formats
url: redaction/java/get-supported-file-formats
title: Get supported file formats
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Get supported file formats

GroupDocs.Redaction allows to get the list of all supported file formats by these steps:

*   Call *getSupportedFileTypes *of *FileType* class;
*   Enumerate through the collection of *FileType *objects*.*

The following example demonstrates how to get supported file formats list.



```java
Iterable<FileType> supportedFileTypes = FileType.getSupportedFileTypes();
Iterator iterator = supportedFileTypes.iterator();      
while (iterator.hasNext())
{
    FileType fileType = (FileType)iterator.next();
    System.out.println(fileType);
}
```
