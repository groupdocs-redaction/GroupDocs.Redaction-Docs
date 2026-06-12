---
id: save-to-stream
url: redaction/python-net/save-to-stream
title: Save to Stream
weight: 6
description: "This article demonstrates that how to save a document to any custom file at any location on the local disc or a even a Stream"
keywords: save a document to any custom file
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
You might need to save a document to any custom file at any location on the local disc or a even a Stream.

The following example demonstrates how to save a document to any location.

{{< tabs "code-example-save-to-stream" >}}
{{< tab "save_to_stream.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import RasterizationOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.pydrawing import Color


def save_to_stream():
    # Define the color of redaction
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = ReplacementOptions(color)
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)

        if result.status != RedactionStatus.FAILED:
            # Save the document to a stream and convert its pages to images
            ro = RasterizationOptions()
            ro.enabled = True
            with open("./redacted-sample.pdf", "wb") as stream_out:
                redactor.save(stream_out, ro)

            print("Document redacted successfully.\nCheck output in ./redacted-sample.pdf")
        else:
            print("Redaction failed!")


if __name__ == "__main__":
    save_to_stream()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-to-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1024 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-to-stream/save_to_stream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
