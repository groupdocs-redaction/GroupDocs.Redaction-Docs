---
id: text-redactions
url: redaction/java/text-redactions
title: Text redactions
weight: 5
description:  This article explains that how Java redaction API allows you to easily redact data of sensitive or private nature from your documents. You can apply text redaction using exact phrase or regular expression for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: Java, redaction, redact data, text redactions  
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Use exact phrase redaction

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code):



```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }
```

By default, search for exact phase is case insensitive.For a case-sensitive redaction, there is a constructor parameter and corresponding public property:



```java
final Redactor redactor = new Redactor("sample.docx");
try
{
    redactor.apply(new ExactPhraseRedaction("John Doe", true /*isCaseSensitive*/, new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }
```

If you need a color box over the redacted text, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of redacted text:



```java
final Redactor redactor = new Redactor("sample.docx");
try
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    redactor.save();
}
finally { redactor.close(); }
```

You might need to apply redaction to a right-to-left document, such as Arabic or Hebrew. The following example demonstrates how to apply ExactPhraseRedaction to an Arabic PDF document:

```java
final Redactor redactor = new Redactor("Arabic.pdf");
try
{
    ExactPhraseRedaction red = new ExactPhraseRedaction("أﺑﺠﺪ", new ReplacementOptions("[test]"));
    red.setRightToLeft(true);
    redactor.apply(red);
    redactor.save();
}
finally { redactor.close(); }
```

### Use regular expression

Behind the scenes, "exact phrase" redaction works though regular expressions, which are the baseline approach for redaction. In the example below, we redact out any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" with a blue color box:



```java
final Redactor redactor = new Redactor("sample.docx");
try
{
    redactor.apply(new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(java.awt.Color.BLUE)));
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    redactor.save(saveOptions);
}
finally { redactor.close(); }
```

If you need to apply redact a whole paragraph, you might also need to use RegexRedaction. The following example demonstrates how to redact the whole paragraph in a PDF document:

```java
final Redactor redactor = new Redactor("LoremIpsum.pdf");
try
{
    redactor.apply(new RegexRedaction("(Lorem(\n|.)+?urna)", new ReplacementOptions("[test]")));
    SaveOptions saveOptions = new SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    redactor.save(saveOptions);
}
finally { redactor.close(); }
```
