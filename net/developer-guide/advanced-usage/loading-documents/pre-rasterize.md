---
id: pre-rasterize
url: redaction/net/pre-rasterize
title: Pre-rasterize
weight: 5
description: "This article shows how to pre-rasterize a document using the redaction API."
keywords: redaction API
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
In some cases, you might need to pre-rasterize the document before opening it and applying redactions. 

For instance, you might need to use an [ImageAreaRedaction](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.redactions/imagearearedaction/) for a whole page of a document with searchable text and images. In order to do that, you will need to pass the Boolean flag to the [LoadOptions](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.options/loadoptions/) class constructor.

The following example demonstrates how to pre-rasterize a Microsoft Word document:

**C#**

```csharp
bool preRasterize = true;
using (Redactor redactor = new Redactor(@"sample.docx"), new LoadOptions(preRasterize))
{
    // Make changes to the file as a rasterized PDF, e.g. uisng ImageAreaRedaction:
    System.Drawing.Point samplePoint = new System.Drawing.Point(516, 311);
    System.Drawing.Size sampleSize = new System.Drawing.Size(170, 35);
    RedactorChangeLog result = redactor.Apply(new ImageAreaRedaction(samplePoint,
                    new RegionReplacementOptions(System.Drawing.Color.Blue, sampleSize)));
    if (result.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    };
}
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
