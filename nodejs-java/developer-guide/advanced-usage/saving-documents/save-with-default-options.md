---
id: save-with-default-options
url: redaction/nodejs-java/save-with-default-options
title: Save with default options
weight: 5
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The simplest way to save the document is it provide no parameters to Save method. In this case the document will be rasterized to PDF and will have the same name as the original one except its extension (.PDF). The PDF file will be overwritten.

The following example demonstrates usage of Save() method with default options.



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
    // Save the document with default options (convert pages into images, save as PDF)
    redactor.save();
}
finally {
  redactor.close();
}
```
