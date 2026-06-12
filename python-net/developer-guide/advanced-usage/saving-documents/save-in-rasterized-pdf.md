---
id: save-in-rasterized-pdf
url: redaction/python-net/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
description: "This article demonstrates that how to save the document as a rasterized PDF file"
keywords: save the document as a rasterized PDF 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
The following example demonstrates how to save the document as a rasterized PDF file:

{{< tabs "code-example-save-in-rasterized-pdf" >}}
{{< tab "save_in_rasterized_pdf.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def save_in_rasterized_pdf():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the redacted document as a rasterized PDF
        so = SaveOptions()
        so.add_suffix = False
        so.rasterize_to_pdf = True

        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    save_in_rasterized_pdf()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.pdf" >}}  
```text
Binary file (PDF, 1024 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/save_in_rasterized_pdf/sample.pdf)
{{< /tab >}}
{{< /tabs >}}
