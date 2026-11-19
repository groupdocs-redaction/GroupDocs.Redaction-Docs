---
id: text-redactions
url: redaction/java/text-redactions
title: Text redactions
weight: 5
description: Apply text redaction with an exact phrase or regular expression to PDF, Word, Excel, PowerPoint, and other supported formats.
keywords: Java, redaction, ExactPhraseRedaction, RegexRedaction
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
You can redact text with [ExactPhraseRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ExactPhraseRedaction) or [RegexRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/RegexRedaction), using a replacement string or a colored box via [ReplacementOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ReplacementOptions). To limit matches to a page range or area, set filters on `ReplacementOptions` (see [Using redaction filters]({{< ref "redaction/java/developer-guide/advanced-usage/using-redaction-filters/_index.md" >}})).

### Use exact phrase redaction

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code):



{{< tabs "code-example-redact-exact-phrase" >}}
{{< tab "redact_exact_phrase.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try 
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactExactPhrase/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

By default, search for exact phase is case insensitive.For a case-sensitive redaction, there is a constructor parameter and corresponding public property:



{{< tabs "code-example-redact-case-sensitive-phrase" >}}
{{< tab "redact_case_sensitive_phrase.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try
{
    redactor.apply(new ExactPhraseRedaction("John Doe", true /*isCaseSensitive*/, new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactCaseSensitivePhrase/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

If you need a color box over the redacted text, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of redacted text:



{{< tabs "code-example-redact-with-color-box" >}}
{{< tab "redact_with_color_box.java" >}}
```java
final Redactor redactor = new Redactor("sample.docx");
try
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    redactor.save();
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1003 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactWithColorBox/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

You might need to apply redaction to a right-to-left document, such as Arabic or Hebrew. The following example demonstrates how to apply ExactPhraseRedaction to an Arabic PDF document:

{{< tabs "code-example-redact-right-to-left-text" >}}
{{< tab "redact_right_to_left_text.java" >}}
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
{{< /tab >}}
{{< tab "arabic.pdf" >}}
{{< tab-text >}}
`arabic.pdf` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/arabic.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Arabic_Redacted.pdf" >}}  
```text
Binary file (PDF, 318 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactRightToLeftText/Arabic_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use regular expression

Behind the scenes, "exact phrase" redaction works though regular expressions, which are the baseline approach for redaction. In the example below, we redact out any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" with a blue color box:



{{< tabs "code-example-redact-with-regex" >}}
{{< tab "redact_with_regex.java" >}}
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
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactWithRegex/sample_Redacted.docx)
{{< /tab >}}
{{< /tabs >}}

If you need to apply redact a whole paragraph, you might also need to use RegexRedaction. The following example demonstrates how to redact the whole paragraph in a PDF document:

{{< tabs "code-example-redact-whole-paragraph" >}}
{{< tab "redact_whole_paragraph.java" >}}
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
{{< /tab >}}
{{< tab "sample.pdf" >}}
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/basic-usage/text-redactions/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "LoremIpsum_Redacted.pdf" >}}  
```text
Binary file (PDF, 2.9 MB)
```
[Download full output](/redaction/java/_output_files/developer-guide/basic-usage/text-redactions/CodeExampleRedactWholeParagraph/LoremIpsum_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
