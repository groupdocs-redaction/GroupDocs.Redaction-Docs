---
id: load-password-protected-file
url: redaction/python-net/load-password-protected-file
title: Load password-protected file
weight: 3
description: "Learn how to load a password-protected file by using .NET redaction API"
keywords: redaction API, load a password-protected file
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
In order to open password-protected documents, you have to pass your password to [LoadOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/) class constructor or assign it to its [Password](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/password/) property of an instance of [LoadOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/) class:

{{< tabs "code-example-load-password-protected-file" >}}
{{< tab "load_password_protected_file.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions, LoadOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def load_password_protected_file():
    # Specify the load options with the document password
    load_opt = LoadOptions("mypassword")

    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the password-protected document to be redacted
    with Redactor("./protected.docx", load_opt) as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the redacted document in its original format
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    load_password_protected_file()
```
{{< /tab >}}
{{< tab "protected.docx" >}}
{{< tab-text >}}
`protected.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/protected.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "protected_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/load_password_protected_file/protected_redacted.docx)
{{< /tab >}}
{{< /tabs >}}
