---
id: image-redactions
url: redaction/java/image-redactions
title: Image redactions
weight: 9
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Redact image area

Although GroupDocs.Redaction for Java does not support OCR at this moment, so you cannot extract text from an image, search it for data and redact sensitive data within the image. You can put a colored box over a given area, such as header, footer, or an area, where customer's data are expected to appear.

In order to do this, you have to use *ImageAreaRedaction* class:



```java
final Redactor redactor  = new Redactor("D:\\test.jpg");
try 
{
    //Define the position on image
    java.awt.Point samplePoint = new java.awt.Point(385, 485);
    //Define the size of the area which need to be redacted
    java.awt.Dimension sampleSize = new java.awt.Dimension(1793, 2069);
    //Perform redaction
    RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(samplePoint,
        new RegionReplacementOptions(java.awt.Color.BLUE, sampleSize)));
    if (result.getStatus() != RedactionStatus.Failed)
    {
       //The redacted output will save as PDF 
       redactor.save();
    };
}
finally { redactor.close(); }
```

If the redaction cannot be applied to this type of files, e.g. MS Word document, *RedactorChangeLog.getStatus()* will be *RedactionStatus.Skipped*.

### Clean image metadata

GroupDocs.Redaction for Java allows you to change image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

The following example demonstrates how to edit exif data (erase them) from a photo or any other image:



```java
final Redactor redactor  = new Redactor("D:\\photo.jpg");
try 
{
    RedactorChangeLog result = redactor.apply(new EraseMetadataRedaction(MetadataFilters.All));
    if (result.getStatus() != RedactionStatus.Failed)
    {
       //The redacted output will save as PDF 
       redactor.save();
    };
}
finally { redactor.close(); }
```

If the redaction cannot be applied to this type of files, e.g. BMP image, *RedactorChangeLog.getStatus()* will be *RedactionStatus.Skipped*.

## Redact embedded images

You can redact image area within all kinds of embedded images inside a document. You have to use *ImageAreaRedaction* class. The following example demonstrates how to redact all embedded images within a Microsoft Word document:



```java
final Redactor redactor = new Redactor("D:\\sample.docx");
try 
{
    java.awt.Point samplePoint = new java.awt.Point(516, 311);
    java.awt.Dimension sampleSize = new java.awt.Dimension(170, 35);
    RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(samplePoint,
        new RegionReplacementOptions(java.awt.Color.BLUE, sampleSize)));
    if (result.getStatus() != RedactionStatus.Failed)
    {
        redactor.save();
    };
}
finally { redactor.close(); }
```

If the redaction cannot be applied to this type of files, e.g. a spreadsheet document, *RedactorChangeLog.getStatus()* will be *RedactionStatus.Skipped*.
