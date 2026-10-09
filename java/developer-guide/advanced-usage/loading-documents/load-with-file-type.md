---
id: load-with-file-type
url: redaction/java/load-with-file-type
title: Load with file type
weight: 6
description: "This article shows how to open a document by explicitly specifying its file type in LoadOptions."
keywords: load options, file type, stream, redaction API
productName: GroupDocs.Redaction for Java
hideChildren: False
---
When you open a document from a [stream]({{< ref "redaction/java/developer-guide/advanced-usage/loading-documents/load-from-stream.md" >}}) without a file name, or when the file extension does not match the actual format, pass the expected format through [LoadOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/loadoptions/) (`LoadOptions(FileType)` or `setFileType`). GroupDocs.Redaction skips automatic format detection and uses the type you specify.

Set the file type to any supported constant from the [FileType](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/filetype/) class, for example `FileType.getDOCX()` or `FileType.getPDF()`. The default value is `FileType.getUnknown()`, which keeps the existing detection behavior.

The following example demonstrates how to load a document from a stream and from a file path while explicitly specifying the file type:

```java
final FileInputStream stream = new FileInputStream("sample.docx");
try
{
    final Redactor redactor = new Redactor(stream, new LoadOptions(FileType.getDOCX()));
    try
    {
        redactor.apply(new DeleteAnnotationRedaction());
        redactor.save();
    }
    finally { redactor.close(); }
}
finally { stream.close(); }

final Redactor redactor = new Redactor("LoremIpsum.pdf", new LoadOptions(FileType.getPDF()));
try
{
    redactor.apply(new ExactPhraseRedaction("Lorem", new ReplacementOptions(java.awt.Color.BLACK)));
    redactor.save();
}
finally { redactor.close(); }
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
