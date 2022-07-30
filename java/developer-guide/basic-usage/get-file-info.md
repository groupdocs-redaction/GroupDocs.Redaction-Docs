---
id: get-file-info
url: redaction/java/get-file-info
title: Get file info
weight: 2
description: This article explains the ability of the GroupDocs.Redaction API to get the general document information, which includes FileType, PageCount and FileSize.
keywords: redaction, java, FileType, PageCount, FileSize
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Get file info

GroupDocs.Redaction provides general document information, which includes:

*   FileType
*   PageCount
*   FileSize

The following code examples demonstrate how to get document information.

### Get file info for a file from local disk



```java
final Redactor redactor = new Redactor(stream);
try 
{
    IDocumentInfo info = redactor.getDocumentInfo();
    System.out.println("\nFile type: " + info.getFileType() + "\nNumber of pages: " + info.getPageCount() + 
            "\nDocument size: " + info.getSize() + " bytes");
}
finally { redactor.close(); }
```

### Get file info for a file from Stream



```java
FileInputStream stream = new FileInputStream("D:\\Sample.docx");
final Redactor redactor = new Redactor("D:\Sample.docx");
try 
{
    IDocumentInfo info = redactor.getDocumentInfo();
    System.out.println("\nFile type: " + info.getFileType() + "\nNumber of pages: " + info.getPageCount() + 
            "\nDocument size: " + info.getSize() + " bytes");
}
finally 
{ 
    redactor.close(); 
    stream.close();
}
```
