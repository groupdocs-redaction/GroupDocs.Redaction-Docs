---
id: save-overwriting-original-file
url: redaction/java/save-overwriting-original-file
title: Save overwriting original file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
The following example demonstrates how to save the redacted document, replacing an original file:



```java
// Make a copy of sample file
Files.copy(new File("Sample.docx").toPath(), new File("OverwrittenSample.docx").toPath(), StandardCopyOption.REPLACE_EXISTING);
// Apply redaction
final Redactor redactor = new Redactor("OverwrittenSample.docx");
try 
{
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    if (result.getStatus() != RedactionStatus.Failed)
    {
        SaveOptions options = new  SaveOptions();
        options.setAddSuffix(false);
        options.setRasterizeToPDF(false);
        // Save the document in original format overwriting original file
        redactor.save(options);
    }
}
finally { redactor.close(); }

```
