---
id: groupdocs-redaction-for-net-23-3-release-notes
url: redaction/net/groupdocs-redaction-for-net-23-3-release-notes
title: GroupDocs.Redaction for .NET 23.3 Release Notes
weight: 10
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for .NET 23.3{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Add support for DjVu files  
*   Add possibility to pre-rasterize documents  
*   Duplicate redaction replacement text in RTF document  
*   ReplacementOption doesn't work when replacement option is a color instead of text  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONNET-227 | Add support for DjVu files | Improvement |
| REDACTIONNET-419 | Add possibility to pre-rasterize documents | Improvement |
| REDACTIONNET-421 | Duplicate redaction replacement text in RTF document | Bug |
| REDACTIONNET-424 | ReplacementOption doesn't work when replacement option is a color instead of text | Bug |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for .NET 23.3. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Add support for DjVu files

This improvement allows users to delete a range of pages or apply image redactions to DjVu documents, saving the result as a PDF file.

### Add possibility to pre-rasterize documents

This improvement allows users to rasterize the documents before applying any redactions.

### Duplicate redaction replacement text in RTF document

This bugfix resolves an issue when the replacement value is duplicated in RTF, OpenOffice and Microsoft Word dcouments.

### ReplacementOption doesn't work when replacement option is a color instead of text

This bugfix resolves a PDF documents issue when no changes are made to the document due to OutOfMemory exception behind the scenes.

##### Public API changes
                                                                                            
Property **PreRasterize**, with a Boolean pre-rasterization flag, has been **added** to **GroupDocs.Redaction.Options.LoadOpions** class.  
Constructor overloads, taking pre-rasterization flag as a parameter, have been **added** to **GroupDocs.Redaction.Options.LoadOpions** class.  

##### Usage

The following example demonstrates how to require pre-rasterization for a Microsoft Word document.
 
**C#**

```csharp
            bool preRasterize = true;
            using (Redactor redactor = new Redactor("Sample.docx"), new LoadOptions(preRasterize))
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

The following example demonstrates how to remove 3 frames from a DjVu document.
 
**C#**

```csharp
            using (Redactor redactor = new Redactor("DrawingScans.djvu"))
            {
                if (redactor.GetDocumentInfo().PageCount > 3)
                {
                    redactor.Apply(new RemovePageRedaction(PageSeekOrigin.Begin, 0, 3));
                    redactor.Save();
                }
            }
```


