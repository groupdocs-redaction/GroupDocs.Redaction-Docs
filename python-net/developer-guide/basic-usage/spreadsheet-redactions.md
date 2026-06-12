---
id: spreadsheet-redactions
url: redaction/python-net/spreadsheet-redactions
title: Spreadsheet redactions
weight: 8
description: This article shows that how Python redaction API allows to redact data of sensitive or private nature from your XLS, XLSX, ODS spreadsheet document formats and others.
keywords: redaction, redact data, xls, xlsx, ods 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction allows to redact data of sensitive or private nature from your XLS, XLSX, ODS spreadsheet document formats and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

## Redact spreadsheet content

{{< tabs "code-example-redact-spreadsheet-content" >}}
{{< tab "redact_spreadsheet_content.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def redact_spreadsheet_content():
    # Specify the redaction options
    repl_opt = ReplacementOptions("-redacted-")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the spreadsheet to be redacted
    with Redactor("./sample.xlsx") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_spreadsheet_content()
```
{{< /tab >}}
{{< tab "sample.xlsx" >}}
{{< tab-text >}}
`sample.xlsx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/spreadsheet-redactions/sample.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.xlsx" >}}  
```text
Binary file (XLSX, 15 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/spreadsheet-redactions/redact_spreadsheet_content/sample_redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}
