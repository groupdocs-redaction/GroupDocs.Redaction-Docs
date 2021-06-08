---
id: save-with-default-options
url: redaction/java/save-with-default-options
title: Save with default options
weight: 5
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
The simplest way to save the document is it provide no parameters to Save method. In this case the document will be rasterized to PDF and will have the same name as the original one except its extension (.PDF). The PDF file will be overwritten.

The following example demonstrates usage of Save() method with default options.



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    // Save the document with default options (convert pages into images, save as PDF)
    redactor.save();
}
finally { redactor.close(); }

```
