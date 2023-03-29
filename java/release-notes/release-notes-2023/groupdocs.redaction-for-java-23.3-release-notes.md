---
id: groupdocs-redaction-for-java-23-3-release-notes
url: redaction/net/groupdocs-redaction-for-java-23-3-release-notes
title: GroupDocs.Redaction for Java 23.3 Release Notes
weight: 10
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 23.3{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Duplicate redaction replacement text in RTF document  
*   ReplacementOption doesn't work when replacement option is a color instead of text  
*   Add possibility to pre-rasterize documents  
*   Add support for DjVu files  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-167 | Duplicate redaction replacement text in RTF document | Bug |
| REDACTIONJAVA-170 | ReplacementOption doesn't work when replacement option is a color instead of text | Bug |
| REDACTIONJAVA-171 | Add possibility to pre-rasterize documents | Improvement |
| REDACTIONJAVA-172 | Add support for DjVu files | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 23.3. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Duplicate redaction replacement text in RTF document

This bugfix resolves an issue when the replacement value is duplicated in RTF, OpenOffice and Microsoft Word dcouments.

### ReplacementOption doesn't work when replacement option is a color instead of text

This bugfix resolves a PDF documents issue when no changes are made to the document due to OutOfMemory exception behind the scenes.

### Add possibility to pre-rasterize documents

This improvement allows users to rasterize the documents before applying any redactions.

### Add support for DjVu files

This improvement allows users to delete a range of pages or apply image redactions to DjVu documents, saving the result as a PDF file.

##### Public API changes
                                                                                            
Methods **getPreRasterize()** and **setPreRasterize()**, getting and setting pre-rasterization flag, have been **added** to **com.groupdocs.redaction.options.LoadOpions** class.  
Constructor overloads, taking pre-rasterization flag as a parameter, have been **added** to **com.groupdocs.redaction.options.LoadOpions** class.  

##### Usage

The following example demonstrates how to require pre-rasterization for a Microsoft Word document.
 
```java
        LoadOptions loadOptions = new LoadOptions(/*preRasterize*/ true);
        final Redactor redactor = new Redactor("sample.docx", loadOptions);
        try 
        {
            // Make changes to the file as a rasterized PDF, e.g. uisng ImageAreaRedaction:
            java.awt.Point samplePoint = new java.awt.Point(516, 311);
            java.awt.Dimension sampleSize = new java.awt.Dimension(170, 35);
            RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(samplePoint,
                new RegionReplacementOptions(java.awt.Color.RED, sampleSize)));
            if (result.getStatus() != RedactionStatus.Failed)
            {
                    redactor.save();
            };
        }
        finally { redactor.close(); }
```

The following example demonstrates how to remove 3 frames from a DjVu document.
 
```java
        final Redactor redactor = new Redactor("DrawingScans.djvu");
        try 
        {
            if (redactor.getDocumentInfo().getPageCount() > 3)
            redactor.apply(new RemovePageRedaction(PageSeekOrigin.Begin, 0, 3));
            redactor.save();
        }
        finally { redactor.close(); }
```


