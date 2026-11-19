---
id: get-file-info
url: redaction/java/get-file-info
title: Get file info
weight: 2
description: This article explains the ability of the GroupDocs.Redaction API to get the general document information, which includes FileType, PageCount and FileSize.
keywords: redaction, java, FileType, PageCount, FileSize
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
### Get file info

GroupDocs.Redaction provides general document information, which includes:

*   FileType
*   PageCount
*   FileSize

The following code examples demonstrate how to get document information.

### Get file info for a file from local disk



{{< tabs "code-example-get-local-file-info" >}}
{{< tab "get_local_file_info.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    IDocumentInfo info = redactor.getDocumentInfo();
    System.out.println("\nFile type: " + info.getFileType() + "\nNumber of pages: " + info.getPageCount() + 
            "\nDocument size: " + info.getSize() + " bytes");
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/get-file-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "code-example-get-local-file-info.txt" >}}  
```text
File type: Microsoft Word Open XML Document (.docx)
Number of pages: 1
Document size: 19370 bytes
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/get-file-info/CodeExampleGetLocalFileInfo/code-example-get-local-file-info.txt)
{{< /tab >}}
{{< /tabs >}}

### Get file info for a file from Stream



{{< tabs "code-example-get-file-info-from-stream" >}}
{{< tab "get_file_info_from_stream.java" >}}
```java
FileInputStream stream = new FileInputStream("sample.docx");
final Redactor redactor = new Redactor(stream);
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
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/get-file-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "code-example-get-file-info-from-stream.txt" >}}  
```text
File type: Microsoft Word Open XML Document (.docx)
Number of pages: 1
Document size: 19370 bytes
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/get-file-info/CodeExampleGetFileInfoFromStream/code-example-get-file-info-from-stream.txt)
{{< /tab >}}
{{< /tabs >}}
