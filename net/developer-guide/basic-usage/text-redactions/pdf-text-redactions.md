---
id: pdf-text-redactions
url: redaction/net/text-redactions/pdf-text-redactions
title: PDF Text redactions
weight: 5
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
GroupDocs.Redaction makes it easy to redact sensitive or private data from your PDF documents. 

With GroupDocs.Redaction API you can apply text redactions to PDF documents using exact phrase match or [regular expressions](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions).

## PDF redaction matching an exact phrase

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code) in a PDF sample file with case-sensitive search:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.pdf"))
{
  redactor.Apply(new ExactPhraseRedaction("John Doe", true /*isCaseSensitive*/, new ReplacementOptions("[personal]")));
  redactor.Save();
}
```

If you need a color box over the redacted PDF file, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of the text:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.pdf"))
{
  redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(System.Drawing.Color.Black)));
  redactor.Save();
}
```

## PDF redaction with regular expressions

In the example below, we remove any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" replacing it with a blue color box from a sample PDF file:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.pdf"))
{
  redactor.Apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(System.Drawing.Color.Blue)));
  redactor.Save();
}
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
