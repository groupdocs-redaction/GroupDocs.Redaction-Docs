---
id: get-file-info
url: redaction/nodejs-java/get-file-info
title: Get file info
weight: 2
description: This article explains the ability of the GroupDocs.Redaction API to get the general document information, which includes FileType, PageCount and FileSize.
keywords: redaction, java, FileType, PageCount, FileSize
productName: GroupDocs.Redaction for Node.js via Java
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



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor(stream);
try 
{
const info = redactor.getDocumentInfo();
    console.log('\nFile type: ' + info.getFileType() + '\nNumber of pages: ' + info.getPageCount() + 
            '\nDocument size: ' + info.getSize() + ' bytes');
}
finally {
  redactor.close();
}
```

### Get file info for a file from Stream



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const stream = new FileInputStream('D:\\Sample.docx');
const redactor = new redaction.Redactor('D:\Sample.docx');
try 
{
const info = redactor.getDocumentInfo();
    console.log('\nFile type: ' + info.getFileType() + '\nNumber of pages: ' + info.getPageCount() + 
            '\nDocument size: ' + info.getSize() + ' bytes');
}
finally 
{ 
    redactor.close(); 
    stream.close();
}
```
