---
id: load-from-local-disc
url: redaction/java/load-from-local-disc
title: Load from local disc
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Load from local disc

*GroupDocs.Redaction.Redactor* class is a main class in Redaction API, providing functionality to open a document. When document is located on the local disk, you can pass its path to *Redactor *class constructor.

The following example demonstrates how to open a document from local disc:



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    // Here we can use document instance to perform redactions   
    redactor.apply(new DeleteAnnotationRedaction());
    redactor.save();
}
finally { redactor.close(); }
```
