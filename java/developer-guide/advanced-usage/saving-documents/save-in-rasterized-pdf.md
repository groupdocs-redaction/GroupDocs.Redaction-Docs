---
id: save-in-rasterized-pdf
url: redaction/java/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
The following example demonstrates how to save the document as a rasterized PDF file:

{{< tabs "code-example-save-in-rasterized-pdf" >}}
{{< tab "save_in_rasterized_pdf.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    SaveOptions tmp0 = new  SaveOptions();
    tmp0.setAddSuffix(true);
    tmp0.setRasterizeToPDF(true);
    tmp0.setRedactedFileSuffix("redacted");
    // Saving as rasterized PDF
    redactor.save(tmp0);
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/CodeExampleSaveInRasterizedPdf/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
