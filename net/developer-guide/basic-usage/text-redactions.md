---
id: text-redactions
url: redaction/net/text-redactions
title: Text redaction
weight: 5
description: This article explains that how C# redaction API allows you to easily redact data of sensitive or private nature from your documents. You can apply text redaction using exact phrase or regular expression for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: c#, redaction, redact data, text redactions  
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
GroupDocs.Redaction allows to easily redact data of sensitive or private nature from your documents. The most popular redaction case is to remove a text from a document.

With GroupDocs.Redaction API you can apply text redaction using exact phrase or [regular expression](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions) for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list at [supported document formats]({{< ref "redaction/net/getting-started/supported-document-formats.md" >}}) article.

## Use exact phrase redaction

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code):

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
  redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
  redactor.Save();
}
```

By default, search for exact phase is case insensitive.For a case-sensitive redaction, there is a constructor parameter and corresponding public property:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
  redactor.Apply(new ExactPhraseRedaction("John Doe", true /*isCaseSensitive*/, new ReplacementOptions("[personal]")));
  redactor.Save();
}
```

If you need a color box over the redacted text, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of redacted text:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
  redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(System.Drawing.Color.Black)));
  redactor.Save();
}
```

You might need to apply redaction to a right-to-left document, such as Arabic or Hebrew. The following example demonstrates how to apply ExactPhraseRedaction to an Arabic PDF document:

**C#**

```csharp
using (Redactor redactor = new Redactor("Arabic.pdf"))
{
    ExactPhraseRedaction red = new ExactPhraseRedaction("أﺑﺠﺪ", new ReplacementOptions("[test]"));
    red.IsRightToLeft = true;
    
    redactor.Apply(red);
    redactor.Save();
}
```

## Use regular expression

Behind the scenes, "exact phrase" redaction works though regular expressions, which are the baseline approach for redaction. In the example below, we redact out any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" with a blue color box:

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
  redactor.Apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(System.Drawing.Color.Blue)));
  redactor.Save();
}
```

If you need to apply redact a whole paragraph, you might also need to use RegexRedaction. The following example demonstrates how to redact the whole paragraph in a PDF document:

**C#**

```csharp
using (Redactor redactor = new Redactor("LoremIpsum.pdf"))
{
    redactor.Apply(new RegexRedaction("(Lorem(\n|.)+?urna)", new ReplacementOptions(System.Drawing.Color.Red)));
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
