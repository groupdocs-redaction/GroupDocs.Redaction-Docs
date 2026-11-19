---
id: save-to-stream
url: redaction/java/save-to-stream
title: Save to stream
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
You might need to save a document to any custom file at any location on the local disc or a even a Stream.

The following example demonstrates how to save a document to any location.



{{< tabs "code-example-save-to-stream" >}}
{{< tab "save_to_stream.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    // Here we can use document instance to perform redactions
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    if (result.getStatus() != RedactionStatus.Failed)
    {
        // Save the document to a stream and convert its pages to images
        final FileOutputStream fileStream = new FileOutputStream("redacted-sample.pdf");
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
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/saving-documents/save-to-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1003 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/saving-documents/save-to-stream/CodeExampleSaveToStream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
