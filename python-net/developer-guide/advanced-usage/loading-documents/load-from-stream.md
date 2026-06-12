---
id: load-from-stream
url: redaction/python-net/load-from-stream
title: Load from Stream
weight: 2
description: "This article shows that how to load file from stream using redaction API"
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
As an alternative to a local file, [Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/) can open a document from stream.

The following example demonstrates how to load and redact a document using Stream:

{{< tabs "code-example-load-from-stream" >}}
{{< tab "load_from_stream.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import RasterizationOptions
from groupdocs.redaction.redactions import DeleteAnnotationRedaction


def load_from_stream():
    # Specify the redaction options - remove all annotations
    del_red = DeleteAnnotationRedaction()

    # Load the document as a stream to be redacted
    with open("./sample.docx", "rb") as stream_in:
        with Redactor(stream_in) as redactor:

            # Apply the redaction
            redactor.apply(del_red)

            # Save the redacted document to a stream as a rasterized PDF
            with open("./redacted-sample.pdf", "wb") as stream_out:
                ro = RasterizationOptions()
                redactor.save(stream_out, ro)
                print("Document redacted successfully.")


if __name__ == "__main__":
    load_from_stream()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/load-from-stream/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 1.2 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/load-from-stream/load_from_stream/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}
