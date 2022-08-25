---
id: groupdocs-redaction-for-net-22-8-release-notes
url: redaction/net/groupdocs-redaction-for-net-22-8-release-notes
title: GroupDocs.Redaction for .NET 22.8 Release Notes
weight: 5
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for .NET 22.8{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Supported frameworks versions changed to .NET 4.5, Net Standard 2.1 and .NET 6.0  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONNET-413 | Provide .NET Standard 2.1 and .NET 6.0 Support | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for .NET 22.8. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Provide .NET Standard 2.1 and .NET 6.0 Support

Supported frameworks versions changed to .NET 4.5, Net Standard 2.1 and .NET 6.0.

##### Public API changes
                                                                                            
There are no changes in public API.

##### Usage

The following example demonstrates how to remove two pages starting from a second one in a PDF file.
 
**C#**

```csharp
            using (Redactor redactor = new Redactor("Sample.pdf"))
            {
                // Requires at least 4 pages
                if (redactor.GetDocumentInfo().PageCount >= 4)
                {
                    redactor.Apply(new RemovePageRedaction(PageSeekOrigin.Begin, 1, 2));
                    redactor.Save(new SaveOptions() { AddSuffix = true, RasterizeToPDF = false });
                }
            }
```



