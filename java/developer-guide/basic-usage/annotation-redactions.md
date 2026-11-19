---
id: annotation-redactions
url: redaction/java/annotation-redactions
title: Annotation redactions
weight: 7
description: This article shows the implementation of annotation redaction for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: annotation, redactions,PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
### Remove annotations (comments etc)

You can use GroupDocs.Redaction to remove all or specific comments and other annotations from the document. For example, we can remove all comments from the document, containing texts like "use", "show" or "describe" in its body:



{{< tabs "code-example-remove-all-annotations" >}}
{{< tab "remove_all_annotations.java" >}}
```java
final Redactor redactor = new Redactor("annotated_sample.xlsx");
try 
{
    redactor.apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));
    SaveOptions options = new  SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    redactor.save(options);
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "annotated.xlsx" >}}
{{< tab-text >}}
`annotated.xlsx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/annotation-redactions/annotated.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annotated_sample_Redacted.xlsx" >}}  
```text
Binary file (XLSX, 12 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/annotation-redactions/CodeExampleRemoveAllAnnotations/annotated_sample_Redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}

You can use constructor without arguments to remove all annotations within the document.

### Redact annotations

Instead of removing all or specific annotations, you can remove sensitive data from the annotation text. For instance, we can remove all mentions of "John" in the given document, e.g.:



{{< tabs "code-example-redact-annotations" >}}
{{< tab "redact_annotations.java" >}}
```java
final Redactor redactor = new Redactor("annotated_sample.xlsx");
try 
{
    redactor.apply(new AnnotationRedaction("(?im:john)", "[redacted]"));
    SaveOptions options = new  SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    redactor.save(options);
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "annotated.xlsx" >}}
{{< tab-text >}}
`annotated.xlsx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/annotation-redactions/annotated.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annotated_sample_Redacted.xlsx" >}}  
```text
Binary file (XLSX, 12 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/annotation-redactions/CodeExampleRedactAnnotations/annotated_sample_Redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}
