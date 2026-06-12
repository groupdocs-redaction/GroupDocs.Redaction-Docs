---
id: load-from-local-disc
url: redaction/python-net/load-from-local-disc
title: Load from local disc
weight: 1
description: "This article shows how the redaction API is used to load file from disk."
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
[GroupDocs.Redaction.Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/) class is a main class in Redaction API, providing functionality to open a document. When document is located on the local disk, you can pass its path to [Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor)  class constructor.

The following example demonstrates how to open a document from local disc:

{{< tabs "code-example-load-from-local-disc" >}}
{{< tab "load_from_local_disc.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import DeleteAnnotationRedaction


def load_from_local_disc():
    # Specify the redaction options - remove all annotations
    del_red = DeleteAnnotationRedaction()

    # Load the document to be redacted from the local disc
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        redactor.apply(del_red)

        # Save the redacted document in its original format next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    load_from_local_disc()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/load-from-local-disc/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/load-from-local-disc/load_from_local_disc/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}
