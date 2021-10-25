---
id: pdf-annotation-redactions
url: redaction/net/annotation-redactions/pdf-annotation-redactions
title: PDF Annotation redactions
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
With GroupDocs.Redaction API you can easily apply annotation redactions to PDF documents to remove sensitive data from annotation text, or completely remove annotations by a regular expression.

## Remove PDF annotations (comments etc)

In this example we remove all annotations from the PDF document, containing texts like "use", "show" or "describe" in its body:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"D:\test.pdf"))
{
   redactor.Apply(new DeleteAnnotationRedaction("(?im:(use|show|describe))"));

   redactor.Save()
}
```

## Redact PDF annotations

In this example, we remove all mentions of "John" in the given PDF document as follows:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"C:\test.pdf"))
{
   redactor.Apply(new AnnotationRedaction("(?im:john)", "[redacted]"));

   redactor.Save()
}
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
