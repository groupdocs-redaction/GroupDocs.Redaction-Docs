---
id: annotation-redactions
url: redaction/java/annotation-redactions
title: Annotation redactions
weight: 7
description: You can apply annotation redactions for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: annotation, redactions,PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Remove annotations (comments etc)

You can use GroupDocs.Redaction to remove all or specific comments and other annotations from the document. For example, we can remove all comments from the document, containing texts like "use", "show" or "describe" in its body:



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

You can use constructor without arguments to remove all annotations within the document.

### Redact annotations

Instead of removing all or specific annotations, you can remove sensitive data from the annotation text. For instance, we can remove all mentions of "John" in the given document, e.g.:



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
