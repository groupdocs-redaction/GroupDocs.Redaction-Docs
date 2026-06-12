---
id: pre-rasterize
url: redaction/python-net/pre-rasterize
title: Pre-rasterize
weight: 5
description: "This article shows how to pre-rasterize a document using the redaction API."
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
In some cases, you might need to pre-rasterize the document before opening it and applying redactions. 

For instance, you might need to use an [ImageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/imagearearedaction/) for a whole page of a document with search-able text and images. In order to do that, you will need to pass the Boolean flag to the [LoadOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/) class constructor.

The following example demonstrates how to pre-rasterize a Microsoft Word document:

{{< tabs "code-example-pre-rasterize-document" >}}
{{< tab "pre_rasterize_document.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def pre_rasterize_document():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)

        if result.status != RedactionStatus.FAILED:
            # By default, the redacted document is saved in PDF format
            save_options = SaveOptions()
            save_options.add_suffix = True
            save_options.rasterize_to_pdf = True
            save_options.redacted_file_suffix = "redacted"
            result_path = redactor.save(save_options)
            print(f"Document redacted successfully.\nCheck output in {result_path}")
        else:
            print("Redaction failed!")


if __name__ == "__main__":
    pre_rasterize_document()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/pre-rasterize/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1024 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/pre-rasterize/pre_rasterize_document/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
