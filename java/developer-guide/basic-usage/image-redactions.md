---
id: image-redactions
url: redaction/java/image-redactions
title: Image redactions
weight: 9
description: This article shows that how to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others.
keywords: redact data,JPG, PNG, TIFF
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Redact image area

GroupDocs.Redactions prodives a set of features to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others. See full list at [supported document formats]({{< ref "redaction/java/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redaction fr Java since version 21.6 supports two ways of redacting images, both in separate image files and embedded images:
*   You can put a colored box over a given area, such as header, footer, or an area, where customer's data are expected to appear.
*   You can use any 3-rd party OCR engine to process the image, search it for text and redact sensitive data within the image.   

GroupDocs.Redaction for Java also allows you to change image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

## Redact image area

In order to redact image area, you have to use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ImageAreaRedaction) class:

**Java**

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

If the redaction cannot be applied to this type of files, e.g. MS Word document without embedded images, [RedactorChangeLog.getStatus()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/RedactorChangeLog#getStatus()) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/RedactionStatus).

## Redact recognized text from an image

To enable OCR-processing and search for a text using regular expressions, you have to implement [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface and pass the instance to [RedactorSettings](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/RedactorSettings) constructor. For more details, see [OCR Usage Basics]({{< ref "redaction/java/developer-guide/advanced-usage/using-ocr/ocr-usage-basics" >}}) article.

**Java**

```Java
try (Redactor redactor = new Redactor("D:\\test.jpg", new LoadOptions(), new RedactorSettings(new MyCustomOcrConnector())))
{
   RedactorChangeLog result = redactor.apply(new RegexRedaction("\\d{4}", new ReplacementOptions(java.awt.Color.BLUE)));
   if (result.getStatus() != RedactionStatus.Failed)
   {
      redactor.save();
   };
}
```

In the example above **MyCustomOcrConnector** class implements [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface.


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

You can redact image area within all kinds of embedded images inside a document. You can both use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ImageAreaRedaction) class and any type of [TextRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/TextRedaction) (regular expression, exact phrase), if the OCR is enabled in **RedactorSettings** (see [OCR Usage Basics]({{< ref "redaction/java/developer-guide/advanced-usage/using-ocr/ocr-usage-basics" >}}) article). 

The following example demonstrates how to redact all embedded images within a Microsoft Word document:

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
