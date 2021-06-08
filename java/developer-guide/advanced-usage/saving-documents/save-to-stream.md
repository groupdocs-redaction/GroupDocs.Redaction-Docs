---
id: save-to-stream
url: redaction/java/save-to-stream
title: Save to stream
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
You might need to save a document to any custom file at any location on the local disc or a even a Stream.

The following example demonstrates how to save a document to any location.



```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Here we can use document instance to perform redactions
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    if (result.getStatus() != RedactionStatus.Failed)
    {
        // Save the document to a custom location and convert its pages to images
        final FileOutputStream fileStream = new FileOutputStream("C:\\\\Temp\\\\sample_output_file.pdf");
        try 
        {
            RasterizationOptions options = new  RasterizationOptions();
            options.setEnabled(true);
            redactor.save(fileStream, options);
        }
        finally { fileStream.close(); }
    }
}
finally { redactor.close(); }

```
