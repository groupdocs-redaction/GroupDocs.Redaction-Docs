---
id: groupdocs-redaction-for-java-23-2-release-notes
url: redaction/java/groupdocs-redaction-for-java-23-2-release-notes
title: GroupDocs.Redaction for Java 23.2 Release Notes
weight: 11
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 23.2{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats  
*   Implement Advanced Rasterization Options (Scan Effects)  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-165 | Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats | Improvement |
| REDACTIONJAVA-166 | Implement Advanced Rasterization Options (Scan Effects) | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 23.2. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats

This improvement allows users to delete a range of pages (image frames) from word processing (Microsoft Word, OpenOffice Text, RTF, etc.) documents as well as multi-frame images.

### Implement Advanced Rasterization Options (Scan Effects)

This improvement allows users to apply scan-like effects to rasterized files (border, grayscale, random noise and inclune, etc.).

##### Public API changes
                                                                                            
Enumeration **AdvancedRasterizationOptions**, containing list of available options, has been **added** to **com.groupdocs.redaction.options** package.  
Method **addAdvancedOption** and its overload, to add adanced rasterization effects, has been **added** to **com.groupdocs.redaction.options.RasterizationOptions** class.  

##### Usage

The following example demonstrates how to remove 3 frames from an animated GIF image.
 
**Java**

```java
final Redactor redactor = new Redactor("Animated.gif");
try 
{
    // Removes 5 frames starting from 3nd one, requires at least 7 frames
    if (redactor.getDocumentInfo().getPageCount() >= 7)
    {
        redactor.apply(new RemovePageRedaction(PageSeekOrigin.Begin, 2, 5));
        redactor.save();
    }
}
finally { redactor.close(); }
```

The following example demonstrates how to apply the advanced rasterization options to a DOCX file with default settings.
 
**Java**

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt);
    redactor.save(so);
}
finally { redactor.close(); }
```


