---
id: groupdocs-redaction-for-java-21-12-release-notes
url: redaction/net/groupdocs-redaction-for-java-21-12-release-notes
title: GroupDocs.Redaction for Java 21.12 Release Notes
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 21.12{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Add support for custom PDF metadata  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-143 | Add support for custom PDF metadata | Improvement |
| REDACTIONJAVA-157 | Small-sized plain text documents fail to be recognized | Bug |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 21.12. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Add support for custom PDF metadata

This improvement allows users to apply redactions to custom XML metadata within PDF files, including metadata of the embedded image resources.

##### Public API changes
                                                                                            
Method **getCategory()**, returning ID of the embedded resource, has been **added** to **MetadataItem** class.  

##### Usage

The following example demonstrates how to remove strings like "/first.last" (e.g. user name in source file paths) from the embedded images metadata of a PDF file.
 
**Java**

```java
            try (Redactor redactor = new Redactor("FileWithEmbeddedImages.pdf"))
            {
                RedactorChangeLog result = redactor.apply(new MetadataSearchRedaction(@"/([^\./]+\.[^/]+)", "/redacted"));
                if (result.getStatus() != RedactionStatus.Failed)
                {
                    redactor.save(new SaveOptions(false, "Redacted"));
                }
            }
```


