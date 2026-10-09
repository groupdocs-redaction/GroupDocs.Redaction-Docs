---
id: image-redactions
url: redaction/nodejs-java/image-redactions
title: Image redactions
weight: 9
description: Redact sensitive regions and metadata from images such as JPG, PNG, TIFF, BMP, and GIF.
keywords: redact image, JPG, PNG, TIFF, ImageAreaRedaction, PageAreaFilter
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Redact image area

GroupDocs.Redaction provides features to redact sensitive data from images (JPG, PNG, TIFF, BMP, GIF, and others). See the full list in [Supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}).

You can redact images both as separate files and as embedded images inside documents:
*   Put a colored box over a given area (header, footer, or a region where customer data appears).
*   Use a third-party OCR engine to search text on the image and redact matches.

You can also change image metadata (for example edit EXIF or act as an "EXIF eraser") where the format exposes metadata.

For multi-page or layout-aware scenarios, combine image-area redaction with [page filters]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/_index.md" >}}) (`PageRangeFilter`, `PageAreaFilter`). Coordinates follow the page (or visible image) placement when the bitmap size differs from the on-page shape.

## Redact image area

In order to redact image area, you have to use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ImageAreaRedaction) class:

**Node.js**
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const redactor = new redaction.Redactor('D:\\test.jpg');
try 
{
    //Define the position on image
const samplePoint = new Point(385, 485);
    //Define the size of the area which need to be redacted
const sampleSize = new Dimension(1793, 2069);
    //Perform redaction
const result = redactor.apply(new redaction.ImageAreaRedaction(samplePoint,
        new redaction.RegionReplacementOptions(Color.BLUE, sampleSize)));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
       //The redacted output will save as PDF 
       redactor.save();
    };
}
finally {
  redactor.close();
}
```

If the redaction cannot be applied to this type of files, e.g. MS Word document without embedded images, [RedactorChangeLog.getStatus()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/RedactorChangeLog#getStatus()) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/RedactionStatus).

## Redact recognized text from an image

To enable OCR-processing and search for a text using regular expressions, you have to implement [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface and pass the instance to [RedactorSettings](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/RedactorSettings) constructor. For more details, see [OCR Usage Basics]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-ocr/ocr-usage-basics" >}}) article.

**Node.js**
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('D:\\test.jpg', new redaction.LoadOptions(), new redaction.RedactorSettings(new MyCustomOcrConnector()));
try {
const result = redactor.apply(new redaction.RegexRedaction('\\d{4}', new redaction.ReplacementOptions(Color.BLUE)));
   if (result.getStatus() !== redaction.RedactionStatus.Failed)
   {
      redactor.save();
   };

} finally {
  redactor.close();
}
```

In the example above **MyCustomOcrConnector** class implements [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface.


### Clean image metadata

GroupDocs.Redaction for Node.js via Java allows you to change image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

The following example demonstrates how to edit exif data (erase them) from a photo or any other image:



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('D:\\photo.jpg');
try 
{
const result = redactor.apply(new redaction.EraseMetadataRedaction(redaction.MetadataFilters.All));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
       //The redacted output will save as PDF 
       redactor.save();
    };
}
finally {
  redactor.close();
}
```

If the redaction cannot be applied to this type of files, e.g. BMP image, *RedactorChangeLog.getStatus()* will be *RedactionStatus.Skipped*.

## Redact embedded images

You can redact image area within all kinds of embedded images inside a document. You can both use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ImageAreaRedaction) class and any type of [TextRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/TextRedaction) (regular expression, exact phrase), if the OCR is enabled in **RedactorSettings** (see [OCR Usage Basics]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-ocr/ocr-usage-basics" >}}) article). 

The following example demonstrates how to redact all embedded images within a Microsoft Word document:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const redactor = new redaction.Redactor('D:\\sample.docx');
try 
{
const samplePoint = new Point(516, 311);
const sampleSize = new Dimension(170, 35);
const result = redactor.apply(new redaction.ImageAreaRedaction(samplePoint,
        new redaction.RegionReplacementOptions(Color.BLUE, sampleSize)));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
        redactor.save();
    };
}
finally {
  redactor.close();
}
```

If the redaction cannot be applied to this type of files, e.g. a spreadsheet document, *RedactorChangeLog.getStatus()* will be *RedactionStatus.Skipped*.

To limit image redaction to a page range or rectangle, set filters on `ReplacementOptions` or use [PageAreaRedaction]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/use-page-area-redaction.md" >}}).

## Multi-frame images

You can remove frames from a multi-frame image with a given origin and frame count. For additional information look at [remove page redactions]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/remove-page-redactions.md" >}}) article.

Some image formats, such as DjVu documents, require [pre-rasterization]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/loading-documents/pre-rasterize.md" >}}) and further saving in PDF format. 
