---
id: pdf-metadata-redactions
url: redaction/net/metadata-redactions/pdf-metadata-redactions
title: PDF Metadata redactions
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
With GroupDocs.Redaction API you can easily apply metadata redactions to PDF documents.

GroupDocs.Redactions provides a flexible API that allows to replace or clear metadata in PDF files using filters or search by regular expression. You can find the details concerning filters usage in [this article]({{< ref "redaction/net/developer-guide/basic-usage/metadata-redactions/_index.md" >}}).

## Clean PDF metadata

You can replace all or specific metadata in the PDF document with empty (blank or minimal) values using [EraseMetadataRedaction](https://apireference.groupdocs.com/net/redaction/groupdocs.redaction.redactions/erasemetadataredaction) class. The example below blanks out all properties of the PDF document:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"C:\sample.pdf"))
{
   redactor.Apply(new EraseMetadataRedaction(MetadataFilters.All));

   redactor.Save();
}
```

## Redact PDF metadata

You can use [MetadataSearchRedaction](https://apireference.groupdocs.com/net/redaction/groupdocs.redaction.redactions/metadatasearchredaction) to remove sensitive data from your PDF document's metadata using regular expressions. For instance, we can remove any mention of "Company Ltd.":

**C#**

```csharp
using (Redactor redactor = new Redactor(@"C:\sample.pdf"))
{
   redactor.Apply(new MetadataSearchRedaction("Company Ltd.", "--company--"));

   redactor.Save();
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
