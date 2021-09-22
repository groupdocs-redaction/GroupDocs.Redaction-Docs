---
id: groupdocs-redaction-for-net-21-9-release-notes
url: redaction/net/groupdocs-redaction-for-net-21-9-release-notes
title: GroupDocs.Redaction for .NET 21.9 Release Notes
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for .NET 21.9{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Add support for custom PDF metadata  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONNET-383 | Add support for custom PDF metadata | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for .NET 21.9. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Add support for custom PDF metadata

This improvement allows users to apply redactions to custom XML metadata within PDF files, including metadata of the embedded image resources.

##### Public API changes
                                                                                            
Property **Category**, containing IDs of the embedded resources, has been **added** to **MetadataItem** class.  

##### Usage

The following example demonstrates how to remove strings like "/first.last" (e.g. user name in source file paths) from the embedded images metadata of a PDF file.
 
**C#**

```csharp
            using (var redactor = new Redactor("FileWithEmbeddedImages.pdf"))
            {
                var result = redactor.Apply(new MetadataSearchRedaction(@"/([^\./]+\.[^/]+)", "/redacted"));
                if (result.Status != RedactionStatus.Failed)
                {
                    redactor.Save(new SaveOptions(false, "Redacted"));
                }
            }
```



