---
id: load-password-protected-file
url: redaction/nodejs-java/load-password-protected-file
title: Load password-protected file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Load password-protected file

In order to open password-protected documents, you have to pass your password to *LoadOptions* class constructor or assign it to its *Password* property of an instance of *LoadOptions* class:



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const loadOptions = new redaction.LoadOptions('mypassword');
const redactor = new redaction.Redactor('protected_sample.docx', loadOptions);
        try 
        {
            // Here we can use document instance to perform redactions
            redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
            redactor.save();
        }
        finally {
  redactor.close();
}
```
