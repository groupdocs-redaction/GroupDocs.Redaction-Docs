---
id: groupdocs-redaction-for-java-20-7-release-notes
url: redaction/java/groupdocs-redaction-for-java-20-7-release-notes
title: GroupDocs.Redaction for Java 20.7 Release Notes
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 20.7{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Ability to redact embedded images in PDF, textual and presentation documents  
    

## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-90 | Implement embedded image redactions in PDF documents | Improvement |
| REDACTIONJAVA-91 | Add support for embedded image redaction with Aspose.Words | Improvement |
| REDACTIONJAVA-92 | Add support for embedded image redaction with Aspose.Slides | Improvement |


## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 20.7. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Allow ImageAreaRedaction to be applied to rasterized PDF

This feature provides functionality to apply ImageAreaRedaction to any embedded image inside PDF document, including resterized PDF files.

### Add support for embedded image redaction with Aspose.Words

This feature provides functionality to apply ImageAreaRedaction to any embedded image inside Microsoft Office Word or Open Office document.

### Add support for embedded image redaction with Aspose.Slides

This feature provides functionality to apply ImageAreaRedaction to any embedded image inside Microsoft Office PowerPoint or Open Office presentation.

##### Public API changes

Obsolete methods **Redactor.getRedactionCallback()** and **Redactor.setRedactionCallback()** have been **removed**.  
Obsolete method **Redactor.isRedactionAccepted(RedactionDescription)** has been **removed**.  

##### Usage

The following example demonstrates how to apply an *ImageAreaRedaction* to all embedded images within a PDF document.
 
```java
final Redactor redactor = new Redactor("D:\\test_with_embedded_images.pdf");
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

The following example demonstrates how to create a rasterized PDF from a Microsoft Word document and apply image redactions to its pages


```java
ByteArrayInputStream inputStream = null;
// Rasterize the document before applying redactions
final Redactor raterizer = new Redactor("C:\\Temp\\sample.docx");
try 
{
    // Perform annotation and textual redactions, if needed
    ByteArrayOutputStream stream = new ByteArrayOutputStream();
    RasterizationOptions options = new RasterizationOptions();
    options.setEnabled(true);
    raterizer.save(stream, options);
    inputStream = new ByteArrayInputStream(stream.toByteArray());  
    stream.close();
}
finally { raterizer.close(); }
if (inputStream != null)
{
    // Re-open the rasterized PDF document to redact its pages as images
    final Redactor redactor = new Redactor(inputStream);
    try 
    {
        RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(new java.awt.Point(1160, 2375),
            new RegionReplacementOptions(java.awt.Color.BLUE, new java.awt.Dimension(1050, 720))));
        if (result.getStatus() != RedactionStatus.Failed)
        {
            final FileOutputStream fileStream = new FileOutputStream("C:\\Temp\\sample_docx_Raster.pdf");
            try 
            {
                RasterizationOptions options = new  RasterizationOptions();
                options.setEnabled(false);
                redactor.save(fileStream, options);
            }
            finally { fileStream.close(); }
        }         
    }
    finally { redactor.close(); inputStream.close(); }
}
```
