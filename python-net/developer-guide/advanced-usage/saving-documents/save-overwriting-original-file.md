---
id: save-overwriting-original-file
url: redaction/python-net/save-overwriting-original-file
title: Save overwriting original file
weight: 3
description: "This article demonstrates that how to save the redacted document, replacing an original file"
keywords: save the redacted document, redacted document
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
The following example demonstrates how to save the redacted document, replacing an original file:

{{< tabs "code-example-save-overwriting-original-file" >}}
{{< tab "save_overwriting_original_file.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.redaction.options.drawing import Color


def save_overwriting_original_file():
    # Define the color of redaction
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = ReplacementOptions(color)
    ex_red = ExactPhraseRedaction("Emily Johnson", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)

        if result.status != RedactionStatus.FAILED:
            # Save the redacted document, overwriting the original file
            so = SaveOptions()
            so.add_suffix = False
            so.rasterize_to_pdf = False
            result_path = redactor.save(so)
            print(f"Document redacted successfully.\nCheck output in {result_path}")
        else:
            print("Redaction failed!")


if __name__ == "__main__":
    save_overwriting_original_file()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example; the example overwrites it. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-overwriting-original-file/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.docx" >}}  
```text
Binary file (DOCX, 41 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-overwriting-original-file/save_overwriting_original_file/sample.docx)
{{< /tab >}}
{{< /tabs >}}
