---
id: save-overwriting-original-file
url: redaction/nodejs-java/save-overwriting-original-file
title: Save overwriting original file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The following example demonstrates how to save the redacted document, replacing an original file:



```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

// Make a copy of sample file
Files.copy(new File('Sample.docx').toPath(), new File('OverwrittenSample.docx').toPath(), StandardCopyOption.REPLACE_EXISTING);
// Apply redaction
const redactor = new redaction.Redactor('OverwrittenSample.docx');
try 
{
const result = redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions(Color.RED)));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
const options = new redaction.SaveOptions();
        options.setAddSuffix(false);
        options.setRasterizeToPDF(false);
        // Save the document in original format overwriting original file
        redactor.save(options);
    }
}
finally {
  redactor.close();
}
```
