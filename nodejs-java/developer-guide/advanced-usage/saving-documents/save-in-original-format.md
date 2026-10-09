---
id: save-in-original-format
url: redaction/nodejs-java/save-in-original-format
title: Save in original format
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The following example demonstrates how to save file in its original format with current date as a suffix:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
const saveOptions = new redaction.SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    saveOptions.setRedactedFileSuffix(new SimpleDateFormat('dd-MM-yyyy').format(new Date()));
    // Saving in original format with date as DateTime.getNow().toShortDateString()a suffix
    redactor.save(saveOptions);
}
finally {
  redactor.close();
}
```
