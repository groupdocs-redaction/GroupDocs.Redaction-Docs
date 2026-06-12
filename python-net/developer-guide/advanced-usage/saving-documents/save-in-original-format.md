---
id: save-in-original-format
url: redaction/python-net/save-in-original-format
title: Save in original format
weight: 1
description: "This article demonstrates that how to save file in its original format with current date as a suffix"
keywords: save file in its original format
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
The following example demonstrates how to save file in its original format with current date as a suffix:

{{< tabs "code-example-save-in-original-format" >}}
{{< tab "save_in_original_format.py" >}}
```python
from datetime import datetime

from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def save_in_original_format():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the redacted document in its original format with the current date as a suffix
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        date_time_str = datetime.now().strftime("%Y-%m-%d %H-%M-%S")
        so.redacted_file_suffix = date_time_str

        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    save_in_original_format()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-in-original-format/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_2026-06-11 17-10-50.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-in-original-format/save_in_original_format/sample_2026-06-11 17-10-50.docx)
{{< /tab >}}
{{< /tabs >}}
