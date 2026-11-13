---
id: quick-start-guide
url: redaction/python-net/quick-start-guide
title: Quick Start Guide
linkTitle: Quick Start Guide
second_title: A simple example of how to use GroupDocs.Redaction for Python via .NET
weight: 4
keywords: quick start, get started, redact, redaction, exact phrase, regular expression, metadata, docx, pdf, xlsx, pip install, venv, virtual environment, GroupDocs.Redaction, python
description: "Set up a virtual environment, install groupdocs-redaction-net, and run three minimal examples: redact a name in a Word document, black out account numbers in a PDF, and clean a spreadsheet of a name and its metadata."
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

This guide shows how to set up GroupDocs.Redaction for Python via .NET and run your first redactions. The library finds sensitive text, metadata, comments and image areas in documents and removes or replaces them, so the saved document no longer contains them.

## Prerequisites

To proceed, make sure you have:

1. **Configured** environment as described in the [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) topic.
2. **Optionally** you may [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/) to test all the product features.

## Set Up Your Development Environment

For best practices, use a virtual environment to manage dependencies in Python applications. Learn more about virtual environments at the [Create and Use Virtual Environments](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments) documentation topic.

### Create and Activate a Virtual Environment

Create a virtual environment:

{{< tabs "example1">}}
{{< tab "Windows" >}}
```ps
py -m venv .venv
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< /tabs >}}

Activate a virtual environment:

{{< tabs "example2">}}
{{< tab "Windows" >}}
```ps
.venv\Scripts\activate
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< /tabs >}}

### Install `groupdocs-redaction-net` Package

After activating the virtual environment, run the following command in your terminal to install the latest version of the package:

{{< tabs "example3">}}
{{< tab "Windows" >}}
```ps
py -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< /tabs >}}

Ensure the package is installed successfully. pip installs `groupdocs-shared-net`, the package of the shared `groupdocs.pydrawing` and `groupdocs.pycore` modules, with it. You should see the message

```bash
Successfully installed groupdocs-redaction-net-* groupdocs-shared-net-*
```

## Example 1: Redact a name in a Word document

The complaint letter `sample.docx` names the customer, Emily Johnson, twice. The example replaces the name with `[customer]` and saves the letter as a Word document:

{{< tabs "demo_app_redact_phrase">}}
{{< tab "redact_phrase.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def redact_phrase():
    with Redactor("sample.docx") as redactor:
        # Replace every occurrence of the name with a label
        result = redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[customer]")))
        print("Status:", result.status.name)

        # Keep the Word format and add a suffix to the file name
        options = SaveOptions()
        options.add_suffix = True
        options.rasterize_to_pdf = False
        options.redacted_file_suffix = "redacted"
        print("Saved to", redactor.save(options))


if __name__ == "__main__":
    redact_phrase()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/getting-started/quick-start-guide/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 40 KB)
```
[Download full output](/redaction/python-net/_output_files/getting-started/quick-start-guide/redact_phrase/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_redact_phrase">}}
{{< tab "Windows" >}}
```ps
py redact_phrase.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 redact_phrase.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 redact_phrase.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation

- `Redactor("sample.docx")`: Opens the document. Use it in a `with` block, so the file is released when you are done.
- `ExactPhraseRedaction(phrase, ReplacementOptions(text))`: Finds the phrase, ignoring case, and replaces it with the text. Pass `True` as the second argument for a case-sensitive search.
- `apply(...)`: Runs the redaction and returns a change log; its `status` is `APPLIED`, `PARTIALLY_APPLIED`, `SKIPPED` or `FAILED`.
- `SaveOptions`: `rasterize_to_pdf = False` keeps the original format; `add_suffix` and `redacted_file_suffix` name the output `sample_redacted.docx`, next to the source.

## Example 2: Black out account numbers in a PDF

The customer statement `sample.pdf` holds an account number such as `12 34 567890`. A regular expression finds it, and a black box covers it:

{{< tabs "demo_app_redact_account_numbers">}}
{{< tab "redact_account_numbers.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options.drawing import Color
from groupdocs.redaction.redactions import RegexRedaction, ReplacementOptions


def redact_account_numbers():
    with Redactor("sample.pdf") as redactor:
        # Two digits, two digits, then six digits: "12 34 567890"
        pattern = r"\d{2}\s*\d{2}[^\d]*\d{6}"
        result = redactor.apply(RegexRedaction(pattern, ReplacementOptions(Color.black)))
        print("Status:", result.status.name)

        # The default save writes a PDF of page images, from which no text can be recovered
        print("Saved to", redactor.save())


if __name__ == "__main__":
    redact_account_numbers()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/getting-started/quick-start-guide/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 914 KB)
```
[Download full output](/redaction/python-net/_output_files/getting-started/quick-start-guide/redact_account_numbers/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

### Explanation

- `RegexRedaction(pattern, options)`: Redacts every match of a regular expression, in .NET syntax.
- `ReplacementOptions(Color.black)`: Draws a box of that colour over the match instead of replacing its text. `Color` comes from `groupdocs.redaction.options.drawing`, with `Point`, `Size` and `Rectangle`.
- `save()`: With no options, saves a rasterized PDF with the `_Redacted` suffix, `sample_Redacted.pdf`. Each page becomes an image, so the covered text is gone from the file, not only hidden.

## Example 3: Clean a spreadsheet of a name and its metadata

`apply()` also takes a list. This example replaces the customer's name in the delivery log `sample.xlsx` and erases the workbook's metadata, such as its author and company, in one call:

{{< tabs "demo_app_redact_spreadsheet">}}
{{< tab "redact_spreadsheet.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import (
    EraseMetadataRedaction,
    ExactPhraseRedaction,
    MetadataFilters,
    ReplacementOptions,
)


def redact_spreadsheet():
    with Redactor("sample.xlsx") as redactor:
        log = redactor.apply([
            ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[customer]")),
            EraseMetadataRedaction(MetadataFilters.ALL),
        ])
        # One log entry per redaction
        for entry in log.redaction_log:
            print(entry.result.status.name)

        # Keep the Excel format, with the "redacted" suffix
        print("Saved to", redactor.save(SaveOptions(False, "redacted")))


if __name__ == "__main__":
    redact_spreadsheet()
```
{{< /tab >}}
{{< tab "sample.xlsx" >}}
{{< tab-text >}}
`sample.xlsx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/getting-started/quick-start-guide/sample.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.xlsx" >}}  
```text
Binary file (XLSX, 8 KB)
```
[Download full output](/redaction/python-net/_output_files/getting-started/quick-start-guide/redact_spreadsheet/sample_redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}

### Explanation

- `apply([...])`: Applies the redactions in order and returns one change log, with an entry per redaction in `redaction_log`.
- `EraseMetadataRedaction(MetadataFilters.ALL)`: Clears every metadata property; a filter such as `MetadataFilters.AUTHOR` clears one.
- `SaveOptions(False, "redacted")`: Keeps the format and adds the suffix: `sample_redacted.xlsx`.

## Next Steps

- [Redaction basics]({{< ref "redaction/python-net/developer-guide/basic-usage/redaction-basics.md" >}}): how redactions, options and results fit together.
- [Text redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/text-redactions.md" >}}): phrases, regular expressions, colours and right-to-left text.
- [Supported Document Formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}): the 40+ formats and what each one supports.
- [Licensing and Evaluation]({{< ref "redaction/python-net/getting-started/licensing-and-subscription.md" >}}): what evaluation mode allows, and how to apply a license.
