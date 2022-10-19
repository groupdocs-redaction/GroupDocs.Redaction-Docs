---
id: groupdocs-redaction-for-java-22-10-release-notes
url: redaction/java/groupdocs-redaction-for-java-22-10-release-notes
title: GroupDocs.Redaction for Java 22.10 Release Notes
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 22.10{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Redacting CSV - IDs are represented in scienifical notation  
*   CSV file with only one data item fails to open  
*   Implement Remove Page Redactions  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-158 | Redacting CSV - IDs are represented in scienifical notation | Bug |
| REDACTIONJAVA-159 | CSV file with only one data item fails to open | Bug |
| REDACTIONJAVA-163 | Implement Remove Page Redactions | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 22.10. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Redacting CSV - IDs are represented in scienifical notation

This bug fix makes GroupDocs.Redaction for Java consider spreadsheet files as textual documents, without transforming large numbers to scientific notation, etc.

### CSV file with only one data item fails to open

This bug fix allows users to treat CSV file with only one data item as a spreadsheet with GroupDocs.Redaction for Java.

### Implement Remove Page Redactions

This improvement allows users to delete a range of pages (slides, worksheets) from PDF documents, spreadsheets and presentations.


##### Public API changes
                                                                                            
Interface **IPaginatedDocument**, declaring methods required to support page deletion, has been **added** to **com.groupdocs.redaction.integration** package.  
Enumeration **PageSeekOrigin**, containing page seek options, has been **added** to **com.groupdocs.redaction.redactions** package.  
Class **RemovePageRedaction**, implementing page remove redactions, has been **added** to **com.groupdocs.redaction.redactions** package.  

##### Usage

The following example demonstrates how to remove the last page from a PDF file.
 
```java
final Redactor redactor  = new Redactor("Contract.pdf");
try 
{
    // Requires at least 1 page
    if (redactor.getDocumentInfo().getPageCount() >= 1)
    {
        redactor.apply(new RemovePageRedaction(PageSeekOrigin.End, 0, 1));
        SaveOptions tmp0 = new  SaveOptions();
        tmp0.setAddSuffix(true);
        tmp0.setRasterizeToPDF(false);
        redactor.save(tmp0);
    }
}
finally { redactor.close(); }
```



