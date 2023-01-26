---
id: groupdocs-redaction-for-net-23-1-release-notes
url: redaction/net/groupdocs-redaction-for-net-23-1-release-notes
title: GroupDocs.Redaction for .NET 23.1 Release Notes
weight: 12
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for .NET 23.1{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats  
*   Implement Advanced Rasterization Options (Scan Effects)  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONNET-415 | Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats | Improvement |
| REDACTIONNET-416 | Implement Advanced Rasterization Options (Scan Effects) | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for .NET 23.1. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Implement Page Removal Functionality for Word Processing and Multi-frame Image Formats

This improvement allows users to delete a range of pages (image frames) from word processing (Microsoft Word, OpenOffice Text, RTF, etc.) documents as well as multi-frame images.

### Implement Advanced Rasterization Options (Scan Effects)

This improvement allows users to apply scan-like effects to rasterized files (border, grayscale, random noise and inclune, etc.).

##### Public API changes
                                                                                            
Enumeration **AdvancedRasterizationOptions**, containing list of available options, has been **added** to **GroupDocs.Redaction.Options** namespace.  
Method **AddAdvancedOption** and its overload, to add adanced rasterization effects, has been **added** to **GroupDocs.Redaction.Options.RasterizationOptions** class.  

##### Usage

The following example demonstrates how to remove 3 frames from an animated GIF image.
 
**C#**

```csharp
            using (Redactor redactor = new Redactor("Animated.gif"))
            {
                // Removes 5 frames starting from 3nd one, requires at least 7 frames
                if (redactor.GetDocumentInfo().PageCount >= 7)
                {
                    redactor.Apply(new RemovePageRedaction(PageSeekOrigin.Begin, 2, 5));
                    redactor.Save();
                }
            }
```

The following example demonstrates how to apply the advanced rasterization options to a DOCX file with default settings.
 
**C#**

```csharp
            using (Redactor redactor = new Redactor("Sample.docx"))
            {
                // Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
                var so = new SaveOptions();
                so.Rasterization.Enabled = true;
                so.RedactedFileSuffix = "_scan";
                so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Border);
                so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Noise);
                so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Grayscale);
                so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Tilt);
                redactor.Save(so);
            }
```


