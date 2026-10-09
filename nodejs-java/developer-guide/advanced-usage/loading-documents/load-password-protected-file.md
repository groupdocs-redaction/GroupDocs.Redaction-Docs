---
id: load-password-protected-file
url: redaction/nodejs-java/load-password-protected-file
title: Load password-protected file
weight: 3
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const loadOptions = new redaction.LoadOptions('mysecretpassword');
const redactor = new redaction.Redactor('protected.docx', loadOptions);
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```
