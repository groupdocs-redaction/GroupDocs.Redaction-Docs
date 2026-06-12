---
id: hello-world
url: redaction/python-net/hello-world
title: Hello, World!
second_title: Basic Example of Using GroupDocs.Redaction for Python via .NET
linkTitle: Hello World
weight: 2
keywords: "hello world, example, get started"
description: Quickly get started with GroupDocs.Redaction for Python via .NET by creating and running a simple example.
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

## Introduction
A "Hello, World!" example is often the first step when exploring GroupDocs.Redaction for Python via .NET. It serves as a simple test to confirm that your development environment is correctly set up and that the library is functioning as expected.

## Overview
GroupDocs.Redaction for Python via .NET lets you search, redact, and remove sensitive information from various document formats. A wide range of [supported formats](/redaction/python-net/getting-started/supported-document-formats/) makes it versatile for different use cases.

## How to redact a document
The following steps demonstrate how to redact sensitive information from a document using GroupDocs.Redaction for Python via .NET:

1. Import the `groupdocs.redaction` classes you need.
2. Describe the redaction (here, an exact phrase to replace with a colored box).
3. Instantiate a `Redactor` with the path to the sample document.
4. Apply the redaction.
5. Save the result.

## Complete example
The example below replaces every occurrence of the phrase "John Doe" with a semi-transparent red box and saves the redacted document:

{{< tabs "code-example-hello-world" >}}
{{< tab "hello_world.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.pydrawing import Color

def hello_world():
    # Draw a semi-transparent red box over every occurrence of "John Doe"
    options = ReplacementOptions(Color.from_argb(128, 255, 0, 0))
    redaction = ExactPhraseRedaction("John Doe", options)

    # Load the document, apply the redaction, and save the result
    with Redactor("./sample.docx") as redactor:
        redactor.apply(redaction)
        save_options = SaveOptions()
        save_options.add_suffix = True
        save_options.rasterize_to_pdf = True
        save_options.redacted_file_suffix = "redacted"
        result_path = redactor.save(save_options)

    print(f"Document redacted successfully. Output saved to {result_path}.")

if __name__ == "__main__":
    hello_world()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/getting-started/hello-world/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/python-net/_output_files/getting-started/hello-world/hello_world/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

This example rasterizes the result to a PDF named `sample_redacted.pdf`, so the redacted content cannot be recovered (`save()` rasterizes to PDF by default; the `redacted_file_suffix` option just controls the output name). To keep the original format instead, set `rasterize_to_pdf = False`.

## Additional resources
This demo references the GroupDocs.Redaction for Python via .NET [code samples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET/).
