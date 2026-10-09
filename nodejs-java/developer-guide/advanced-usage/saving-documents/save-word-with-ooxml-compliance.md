---
id: save-word-with-ooxml-compliance
url: redaction/nodejs-java/save-word-with-ooxml-compliance
title: Save Word with OOXML compliance
weight: 8
description: "This article shows how to save a Word processing document with a specific OOXML compliance level after redaction."
keywords: Word processing OOXML compliance
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
When saving a word processing document in its original format, you can set the OOXML compliance level through [SaveOptions.getWordprocessingSaveOptions().setOoxmlCompliance](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/wordprocessingsaveoptions/). Use values from the [WordProcessingComplianceLevel](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/wordprocessingcompliancelevel/) enumeration: `Ecma`, `Transitional`, or `Strict`.

If you do not set this property, GroupDocs.Redaction preserves the compliance level of the original document. The Strict compliance level can only be downgraded to Transitional, not to Ecma.

This option applies to OOXML-based Word formats such as DOCX, DOCM, DOTX, and DOTM. Set `RasterizeToPDF` to `false` to save the document in its original Word format instead of as a rasterized PDF.

The following example demonstrates how to save a redacted Word document with the Strict OOXML compliance level:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try
{
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
const options = new redaction.SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    options.setRedactedFileSuffix('Strict');
    // If not specified, the compliance level of the original document is preserved.
    options.getWordprocessingSaveOptions().setOoxmlCompliance(redaction.WordProcessingComplianceLevel.Strict);

    redactor.save(options);
}
finally {
  redactor.close();
}
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Node.js via Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
