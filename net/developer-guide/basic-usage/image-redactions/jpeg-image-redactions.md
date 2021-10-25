---
id: jpeg-image-redactions
url: redaction/net/image-redactions/jpeg-image-redactions
title: JPEG Image redactions
weight: 9
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
GroupDocs.Redactions prodives two ways to remove sensitive data from JPEG image files: putting a colored box over a given area or using any 3-rd party OCR engine to process the image and search it for text. For more information, please, look at [this article]({{< ref "redaction/net/developer-guide/basic-usage/image-redactions/_index.md" >}})

GroupDocs.Redaction for .NET also allows you to change JPEG image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

## Redact JPEG image area

You can redact an area in standalone and embedded JPEG images. In this example we redact a JPEG image area with dimensions 170x35 px, located at X = 516, Y = 311, with a blue rectangle:

**C#**

```csharp
using (Redactor redactor = new Redactor("D:\\test.jpeg"))
{
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

## Redact recognized text from a JPEG image

You can enable OCR-processing and search for a text using regular expressions in your JPEG file or an embedded JPEG image. For more details, see [OCR Usage Basics]({{< ref "redaction/net/developer-guide/advanced-usage/using-ocr/ocr-usage-basics" >}}) article.

**C#**

```csharp
using (Redactor redactor = new Redactor("D:\\test.jpeg", new LoadOptions(), new RedactorSettings(new MyCustomOcrConnector())))
{
   RedactorChangeLog result = redactor.Apply(new RegexRedaction("\\d{4}", new ReplacementOptions(System.Drawing.Color.Blue)));
   if (result.Status != RedactionStatus.Failed)
   {
      redactor.Save();
   };
}
```

## Clean JPEG image metadata

The following example demonstrates how to edit EXIF data (erase them) from a JPEG image:

**C#**

```csharp
using (Redactor redactor = new Redactor("D:\\photo.jpeg"))
{
    redactor.Apply(new EraseMetadataRedaction(MetadataFilters.All));
    // Save the document to "*_Redacted.*" file in original format
    redactor.Save(new SaveOptions() { AddSuffix = true, RasterizeToPDF = false });
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
