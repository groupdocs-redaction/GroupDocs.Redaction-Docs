---
id: text-redactions
url: redaction/nodejs-java/text-redactions
title: Text redactions
weight: 5
description: "Exact phrase and regex text redaction in Node.js via Java."
keywords: ExactPhraseRedaction, RegexRedaction
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Exact phrase

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```

Case-sensitive search:

```js
redactor.apply(new redaction.ExactPhraseRedaction(
  'John Doe',
  true,
  new redaction.ReplacementOptions('[personal]')));
```

### Regular expression

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.RegexRedaction(
    '\\d{2,}',
    new redaction.ReplacementOptions('[num]')));
  redactor.save();
} finally {
  redactor.close();
}
```
