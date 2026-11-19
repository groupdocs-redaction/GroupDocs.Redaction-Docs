---
id: load-from-stream
url: redaction/java/load-from-stream
title: Load from Stream
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
### Load from Stream

As an alternative to a local file, *Redactor* can open a document from stream.

The following example demonstrates how to load and redact a document using Stream:



{{< tabs "code-example-load-from-stream" >}}
{{< tab "load_from_stream.java" >}}
```java
final FileInputStream stream = new FileInputStream("sample.docx");
try 
{
    final Redactor redactor = new Redactor(stream);
    try 
    {
        // Here we can use document instance to make redactions
        redactor.apply(new DeleteAnnotationRedaction());
        final FileOutputStream outputStream = new FileOutputStream("redacted-sample.pdf");
        try
        {
            RasterizationOptions options = new RasterizationOptions();
            options.setEnabled(true);
            redactor.save(outputStream, options);
        }
        finally { outputStream.close(); }
    }
    finally { redactor.close(); }
}
finally { stream.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/loading-documents/load-from-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1.2 MB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/loading-documents/load-from-stream/CodeExampleLoadFromStream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
