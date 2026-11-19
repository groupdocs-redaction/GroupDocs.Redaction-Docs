---
id: load-password-protected-file
url: redaction/java/load-password-protected-file
title: Load password-protected file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
### Load password-protected file

In order to open password-protected documents, you have to pass your password to *LoadOptions* class constructor or assign it to its *Password* property of an instance of *LoadOptions* class:



{{< tabs "code-example-load-password-protected-file" >}}
{{< tab "load_password_protected_file.java" >}}
```java
        LoadOptions loadOptions = new LoadOptions("mypassword");
        final Redactor redactor = new Redactor("protected_sample.docx", loadOptions);
        try 
        {
            // Here we can use document instance to perform redactions
            redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
            redactor.save();
        }
        finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "protected.docx" >}}
{{< tab-text >}}
`protected.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/protected.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "protected_sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/CodeExampleLoadPasswordProtectedFile/protected_sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
