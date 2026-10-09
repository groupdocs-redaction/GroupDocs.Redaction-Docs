---
id: get-document-page-preview
url: redaction/nodejs-java/get-document-page-preview
title: Get document page preview
weight: 3
description: This article shows the implementation of Redactor class which supports the rendering of the document preview in JPEG, PNG and BMP.
keywords: redactor, jpeg, png, bmp
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

In GroupDocs.Redaction, *Redactor* class supports rendering of the document preview in on of these image formats:

*   JPEG Image
*   Portable Network Graphics
*   Bitmap Image File

The following example demonstrates how to get a single page preview of the document. Preview streaming uses [ICreatePageStream](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/ICreatePageStream) and [PreviewOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/PreviewOptions) from the Java API, wrapped with `java.newProxy`:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const FileOutputStream = java.import('java.io.FileOutputStream');

const testFile = 'sample.docx';
const testPageNumber = 1;
const previewFileName = `sample_page${testPageNumber}.png`;

const createPageStream = java.newProxy('com.groupdocs.redaction.options.ICreatePageStream', {
  createPageStream: function (_pageNumber) {
    return new FileOutputStream(previewFileName);
  }
});

const redactor = new redaction.Redactor(testFile);
try {
  const options = new redaction.PreviewOptions(createPageStream);
  options.setHeight(640);
  options.setWidth(480);
  options.setPageNumbers(java.newArray('int', [testPageNumber]));
  options.setPreviewFormat(redaction.PreviewFormats.Png);
  redactor.generatePreview(options);
  console.log(`Preview for page ${testPageNumber} was saved to "${previewFileName}"`);
} finally {
  redactor.close();
}
```
