---
id: save-with-default-options
url: redaction/python-net/save-with-default-options
title: Save with default options
weight: 4
description: "This article demonstrates the simplest way to save the document"
keywords: simplest way to save the document
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
The simplest way to save the document is it provide no parameters to [Save](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method. In this case the document will be rasterized to PDF and will have the same name as the original one except its extension (.PDF). The PDF file will be overwritten.

The following example demonstrates usage of [Save()](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method with default options.

{{< tabs "code-example-save-with-default-options" >}}
{{< tab "save_with_default_options.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def save_with_default_options():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the document with default options (convert pages into images, save as PDF)
        save_options = SaveOptions()
        save_options.add_suffix = True
        save_options.rasterize_to_pdf = True
        save_options.redacted_file_suffix = "redacted"
        result_path = redactor.save(save_options)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    save_with_default_options()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-with-default-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1024 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-with-default-options/save_with_default_options/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
