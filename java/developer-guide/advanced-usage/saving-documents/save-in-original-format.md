---
id: save-in-original-format
url: redaction/java/save-in-original-format
title: Save in original format
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
The following example demonstrates how to save file in its original format with current date as a suffix:



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    saveOptions.setRedactedFileSuffix(new SimpleDateFormat("dd-MM-yyyy").format(new Date()));
    // Saving in original format with date as DateTime.getNow().toShortDateString()a suffix
    redactor.save(saveOptions);
}
finally { redactor.close(); }
```
