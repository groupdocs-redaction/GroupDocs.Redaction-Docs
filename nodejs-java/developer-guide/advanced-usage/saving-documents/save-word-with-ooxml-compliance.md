---
id: save-word-with-ooxml-compliance
url: redaction/nodejs-java/save-word-with-ooxml-compliance
title: Save Word with OOXML compliance
weight: 8
description: "Set OOXML compliance when saving Word documents in original format."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
Use `SaveOptions.getWordprocessingSaveOptions().setOoxmlCompliance(...)` with `WordProcessingComplianceLevel` (`Ecma`, `Transitional`, `Strict`). If unset, the original compliance is preserved. Strict can only be downgraded to Transitional, not to Ecma. Set `RasterizeToPDF` to `false` to keep the Word format.

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));

  const options = new redaction.SaveOptions();
  options.setAddSuffix(true);
  options.setRasterizeToPDF(false);
  options.setRedactedFileSuffix('Strict');
  options.getWordprocessingSaveOptions().setOoxmlCompliance(
    redaction.WordProcessingComplianceLevel.Strict);

  redactor.save(options);
} finally {
  redactor.close();
}
```
