---
id: save-overwriting-original-file
url: redaction/java/save-overwriting-original-file
title: Save overwriting original file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
The following example demonstrates how to save the redacted document, replacing an original file:



{{< tabs "code-example-save-overwriting-original-file" >}}
{{< tab "save_overwriting_original_file.java" >}}
```java
// Make a copy of sample file
Files.copy(new File("sample.docx").toPath(), new File("OverwrittenSample.docx").toPath(), StandardCopyOption.REPLACE_EXISTING);
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
// Publish a distinct artifact for the docs output tab
Files.copy(new File("OverwrittenSample.docx").toPath(), new File("sample_overwritten.docx").toPath(), StandardCopyOption.REPLACE_EXISTING);
```
{{< /tab >}}
{{< tab "OverwrittenSample.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/saving-documents/save-overwriting-original-file/CodeExampleSaveOverwritingOriginalFile/OverwrittenSample.docx)
{{< /tab >}}
{{< /tabs >}}
