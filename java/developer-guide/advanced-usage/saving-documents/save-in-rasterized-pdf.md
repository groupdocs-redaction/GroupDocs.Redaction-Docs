---
id: save-in-rasterized-pdf
url: redaction/java/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
The following example demonstrates how to save the document as a rasterized PDF file:



```java
final Redactor redactor = new Redactor(Constants.SAMPLE_DOCX);
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    SaveOptions tmp0 = new  SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);
    // Saving as rasterized PDF with no suffix in file name
    redactor.save(tmp0);
}
finally { redactor.close(); }
```
