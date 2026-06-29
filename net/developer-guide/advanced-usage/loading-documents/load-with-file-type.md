---
id: load-with-file-type
url: redaction/net/load-with-file-type
title: Load with file type
weight: 6
description: "This article shows how to open a document by explicitly specifying its file type in LoadOptions."
keywords: load options, file type, stream, redaction API
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
When you open a document from a [stream]({{< ref "redaction/net/developer-guide/advanced-usage/loading-documents/load-from-stream.md" >}}) without a file name, or when the file extension does not match the actual format, pass the expected format through [LoadOptions.FileType](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.options/loadoptions/properties/filetype). GroupDocs.Redaction skips automatic format detection and uses the type you specify.

Set `FileType` to any supported constant from the [FileType](https://reference.groupdocs.com/net/redaction/groupdocs.redaction/filetype) class, for example `FileType.DOCX` or `FileType.PDF`. The default value is `FileType.Unknown`, which keeps the existing detection behavior.

The following example demonstrates how to load a document from a stream and from a file path while explicitly specifying the file type:

**C#**

```csharp
using System.IO;
using GroupDocs.Redaction.Options;
using GroupDocs.Redaction.Options.Drawing;
using GroupDocs.Redaction.Redactions;

string sourceFileStream = @"sample.docx";
using (Stream stream = File.Open(sourceFileStream, FileMode.Open, FileAccess.ReadWrite))
{
    using (Redactor redactor = new Redactor(stream, new LoadOptions(FileType.DOCX)))
    {
        redactor.Apply(new DeleteAnnotationRedaction());
        redactor.Save();
    }
}

string sourceFilePath = @"LoremIpsum.pdf";
using (Redactor redactor = new Redactor(sourceFilePath, new LoadOptions(FileType.PDF)))
{
    redactor.Apply(new ExactPhraseRedaction("Lorem", new ReplacementOptions(Color.Chocolate)));
    redactor.Save();
}
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
  
*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
