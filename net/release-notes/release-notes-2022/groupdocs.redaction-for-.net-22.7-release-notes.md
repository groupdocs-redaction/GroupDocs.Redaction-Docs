---
id: groupdocs-redaction-for-net-22-7-release-notes
url: redaction/net/groupdocs-redaction-for-net-22-7-release-notes
title: GroupDocs.Redaction for .NET 22.7 Release Notes
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for .NET 22.7{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Implement Remove Page Redactions  
*   License not working for GroupDocs.Redaction when other Aspose APIs are installed  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONNET-405 | Implement Remove Page Redactions | Improvement |
| REDACTIONNET-407 | License not working for GroupDocs.Redaction when other Aspose APIs are installed | Bug |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for .NET 22.7. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Implement Remove Page Redactions

This improvement allows users to delete a range of pages (slides, worksheets) from PDF documents, spreadsheets and presentations.

### License not working for GroupDocs.Redaction when other Aspose APIs are installed

This bug fix allows users to use latest versions of Aspose components with GroupDocs.Redaction for .NET.

##### Public API changes
                                                                                            
Interface **IPaginatedDocument**, declaring methods required to support page deletion, has been **added** to **GroupDocs.Redaction.Integration** namespace.  
Enumeration **PageSeekOrigin**, containing page seek options, has been **added** to **GroupDocs.Redaction.Redactions** namespace.  
Class **RemovePageRedaction**, implementing page remove redactions, has been **added** to **GroupDocs.Redaction.Redactions** namespace.  

##### Usage

The following example demonstrates how to remove the last page from a PDF file.
 
**C#**

```csharp
            using (Redactor redactor = new Redactor("Contract.pdf"))
            {
                // Requires at least 1 page
                if (redactor.GetDocumentInfo().PageCount >= 1)
                {
                    redactor.Apply(new RemovePageRedaction(PageSeekOrigin.End, 0, 1));
                    redactor.Save(new SaveOptions() { AddSuffix = true, RasterizeToPDF = false });
                }
            }
```



