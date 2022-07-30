---
id: redaction-basics
url: redaction/java/redaction-basics
title: Redaction Basics
weight: 4
description: This article shows that how Java developers can apply metadata, image, annotation and text redaction in their documents. Wide range of document formats is supported, such as, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: text redaction, java, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX.
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Redaction types

GroupDocs.Redaction comes with the following redaction types:

| Type | Description | Classes |
| --- | --- | --- |
| [Text]({{< ref "redaction/java/developer-guide/basic-usage/redaction-basics.md" >}}) | Replaces or hides with color block a portion of text within document body | *ExactPhraseRedaction*, *RegexRedaction* |
| [Metadata]({{< ref "redaction/java/developer-guide/basic-usage/redaction-basics.md" >}}) | Replace metadata values with empty ones or redacts metadata texts | *EraseMetadataRedaction*, *MetadataSearchRedaction* |
| [Annotations]({{< ref "redaction/java/developer-guide/basic-usage/redaction-basics.md" >}}) | Deletes annotations from document or redacts its texts | *DeleteAnnotationRedaction*, *AnnotationRedaction* |
| [Images]({{< ref "redaction/java/developer-guide/basic-usage/redaction-basics.md" >}}) | Replaces specific area of an image with a colored box | *ImageAreaRedaction* |

### Apply redaction

Applying redaction to a document is done through *Redactor.apply* method. As a result, you receive *RedactorChangeLog* instance, containing a log entry for each redaction applied. The entry contains reference to *Redacton* instance including its options, status of the operation (see below) and textual descriptions when applicable. If at least one redaction failed, you will see *Status* == *RedactionStatus.Failed*:



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }
```

All possible statuses are listed in this table:

| Status | Description | Possible reasons |
| --- | --- | --- |
| *Applied* | Redaction was fully and successfully applied | All operations within redaction process were successfully applied |
| *PartiallyApplied* | Redaction was applied only to a part of its matches | 1) Trial limitations for replacements were exceeded2) At least one change was rejected by user |
| *Skipped* | Redaction was skipped (not applied) | 1) Trial limitations for redactions were exceeded2) Redaction cannot be applied to this type of document3) All replacements were rejected by user and no changes were made |
| *Failed* | Redaction failed with exception | An exception occurred in process of redaction |

For detailed information you have to iterate through redaction log entries in *RedactorChangeLog.RedactionLog* and check for ErrorMessage property of any items with status other than *Applied*:



```java
RedactorChangeLog summary = redactor.apply( ... );
if (result.getStatus() != RedactionStatus.Failed)
{
	for (RedactorLogEntry logEntry : result.getRedactionLog())
    {
        if (logEntry.getResult().getStatus() != RedactionStatus.Applied)
        {
            System.out.println(logEntry.getRedaction().getClass().getName() + " status is " + 
               logEntry.getResult().getStatus() + ", details: " + logEntry.getResult().getErrorMessage());
        }
    }
}
```

### Apply multiple redactions

You can apply as much redactions as you need in a single call to *Redactor.Apply()* method, since its overload accepts an array of redactions and redaction policy. In this case, redactions will be applied in the same order as they appear in the array. As an alternative to specifying redaction sets in your code, you can create an XML file with redaction policy, as described [here]({{< ref "redaction/java/developer-guide/basic-usage/redaction-basics.md" >}}).



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    Redaction[] redactionList = new Redaction[]
    {
          new ExactPhraseRedaction("John Doe", new ReplacementOptions("[Client]")),
          new RegexRedaction("Redaction", new ReplacementOptions("[Product]")),
          new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(java.awt.Color.BLUE)),
          new DeleteAnnotationRedaction(),
          new EraseMetadataRedaction(MetadataFilters.All)
    };
    redactor.apply(redactionList);
    // false, if at least one redaction failed
    if (result.getStatus() != RedactionStatus.Failed)
    {
        redactor.save();
    }
}
finally { redactor.close(); }
```
