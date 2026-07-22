---
id: save-word-with-ooxml-compliance
url: redaction/net/save-word-with-ooxml-compliance
title: Save Word with OOXML compliance
weight: 8
description: "This article shows how to save a Word processing document with a specific OOXML compliance level after redaction."
keywords: Word processing OOXML compliance
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
When saving a word processing document in its original format, you can set the OOXML compliance level through [SaveOptions.WordprocessingSaveOptions.OoxmlCompliance](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.options/wordprocessingsaveoptions/ooxmlcompliance/). Use values from the [WordProcessingComplianceLevel](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.options/wordprocessingcompliancelevel/) enumeration, such as `Ecma`, `Transitional`, or `Strict`.

If you do not set this property, GroupDocs.Redaction preserves the compliance level of the original document. The Strict compliance level can only be downgraded to Transitional, not to Ecma.

This option applies to OOXML-based Word formats such as DOCX, DOCM, DOTX, and DOTM. Set `RasterizeToPDF` to `false` to save the document in its original Word format instead of as a rasterized PDF.

The following example demonstrates how to save a redacted Word document with the Strict OOXML compliance level:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Here we can use document instance to perform redactions
    redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));

    // Save the document
    var options = new SaveOptions()
    {
        AddSuffix = true,
        RasterizeToPDF = false, // original format
        RedactedFileSuffix = "Strict"
    };
    // Set the OOXML compliance level to Strict
    // If not specified, the compliance level of the original document is preserved.
    options.WordprocessingSaveOptions.OoxmlCompliance = WordProcessingComplianceLevel.Strict;

    redactor.Save(options);
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
