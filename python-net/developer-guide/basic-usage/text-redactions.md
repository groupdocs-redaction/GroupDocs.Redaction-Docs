---
id: text-redactions
url: redaction/python-net/text-redactions
title: Text redaction
weight: 5
description: This article explains that how Python redaction API allows you to easily redact data of sensitive or private nature from your documents. You can apply text redaction using exact phrase or regular expression for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: redaction, redact data, text redactions  
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction allows to easily redact data of sensitive or private nature from your documents. The most popular redaction case is to remove a text from a document.

With GroupDocs.Redaction API you can apply text redaction using exact phrase or [regular expression](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions) for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

## Use exact phrase redaction

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code):

{{< tabs "code-example-redact-exact-phrase" >}}
{{< tab "redact_exact_phrase.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def redact_exact_phrase():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_exact_phrase()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_exact_phrase/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

By default, search for exact phase is case insensitive. For a case-sensitive redaction, there is a constructor parameter and corresponding public property:

{{< tabs "code-example-redact-case-sensitive-phrase" >}}
{{< tab "redact_case_sensitive_phrase.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def redact_case_sensitive_phrase():
    # Enable case-sensitive matching
    case_sensitive = True

    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", case_sensitive, repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_case_sensitive_phrase()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_case_sensitive_phrase/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

If you need a color box over the redacted text, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of redacted text:

{{< tabs "code-example-redact-with-color-box" >}}
{{< tab "redact_with_color_box.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.pydrawing import Color


def redact_with_color_box():
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = ReplacementOptions(color)
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_with_color_box()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_with_color_box/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

You might need to apply redaction to a right-to-left document, such as Arabic or Hebrew. The following example demonstrates how to apply ExactPhraseRedaction to an Arabic PDF document:

{{< tabs "code-example-redact-right-to-left-text" >}}
{{< tab "redact_right_to_left_text.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def redact_right_to_left_text():
    # Specify the redaction options with an Arabic phrase
    repl_opt = ReplacementOptions("[test]")
    ex_red = ExactPhraseRedaction("انتقد", repl_opt)

    # Load the document to be redacted
    with Redactor("./arabic.pdf") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_right_to_left_text()
```
{{< /tab >}}
{{< tab "arabic.pdf" >}}
{{< tab-text >}}
`arabic.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/arabic.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "arabic_redacted.pdf" >}}  
```text
Binary file (PDF, 23 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_right_to_left_text/arabic_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

## Use regular expression

Behind the scenes, "exact phrase" redaction works though regular expressions, which are the baseline approach for redaction. In the example below, we redact out any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" with a blue color box:

{{< tabs "code-example-redact-with-regex" >}}
{{< tab "redact_with_regex.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import RegexRedaction, ReplacementOptions
from groupdocs.pydrawing import Color


def redact_with_regex():
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = ReplacementOptions(color)
    reg_red = RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction
        result = redactor.apply(reg_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_with_regex()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_with_regex/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

If you need to apply redact a whole paragraph, you might also need to use RegexRedaction. The following example demonstrates how to redact the whole paragraph in a PDF document:

{{< tabs "code-example-redact-whole-paragraph" >}}
{{< tab "redact_whole_paragraph.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import RegexRedaction, ReplacementOptions
from groupdocs.pydrawing import Color


def redact_whole_paragraph():
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options that match an entire paragraph
    repl_opt = ReplacementOptions(color)
    reg_red = RegexRedaction("(Lorem(\n|.)+?urna)", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.pdf") as redactor:
        # Apply the redaction
        result = redactor.apply(reg_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_whole_paragraph()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/text-redactions/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 68 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/text-redactions/redact_whole_paragraph/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
