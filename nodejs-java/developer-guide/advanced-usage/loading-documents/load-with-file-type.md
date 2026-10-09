---
id: load-with-file-type
url: redaction/nodejs-java/load-with-file-type
title: Load with file type
weight: 6
description: "This article shows how to open a document by explicitly specifying its file type in LoadOptions."
keywords: load options, file type, stream, redaction API
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
When you open a document from a [stream]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/loading-documents/load-from-stream.md" >}}) without a file name, or when the file extension does not match the actual format, pass the expected format through [LoadOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/loadoptions/) (`LoadOptions(FileType)` or `setFileType`). GroupDocs.Redaction skips automatic format detection and uses the type you specify.

Set the file type to any supported constant from the [FileType](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/filetype/) class, for example `FileType.getDOCX()` or `FileType.getPDF()`. The default value is `FileType.getUnknown()`, which keeps the existing detection behavior.

The following example demonstrates how to load a document from a stream and from a file path while explicitly specifying the file type:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const stream = new FileInputStream('sample.docx');
try
{
const redactor = new redaction.Redactor(stream, new redaction.LoadOptions(redaction.FileType.getDOCX()));
    try
    {
        redactor.apply(new redaction.DeleteAnnotationRedaction());
        redactor.save();
    }
    finally {
  redactor.close();
}
}
finally {
  stream.close();
}
const redactor = new redaction.Redactor('LoremIpsum.pdf', new redaction.LoadOptions(redaction.FileType.getPDF()));
try
{
    redactor.apply(new redaction.ExactPhraseRedaction('Lorem', new redaction.ReplacementOptions(Color.BLACK)));
    redactor.save();
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
