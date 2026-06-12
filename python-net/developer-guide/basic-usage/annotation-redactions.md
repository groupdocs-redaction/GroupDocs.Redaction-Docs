---
id: annotation-redactions
url: redaction/python-net/annotation-redactions
title: Annotation redactions
weight: 7
description: This article shows the implementation of annotation redaction for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: annotation, redactions,PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
With GroupDocs.Redaction API you can apply annotation redactions for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redactions provides a flexible API that allows to remove sensitive data from annotation text, or completely remove annotations by a regular expression.

## Remove annotations (comments etc)

You can use GroupDocs.Redaction to remove all or specific comments and other annotations from the document. For example, we can remove all comments from the document, containing texts like "use", "show" or "describe" in its body:

{{< tabs "code-example-remove-all-annotations" >}}
{{< tab "remove_all_annotations.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import DeleteAnnotationRedaction


def remove_all_annotations():
    # Specify the redaction options to delete annotations matching the pattern
    a_red = DeleteAnnotationRedaction("(?im:(use|show|describe))")

    # Load the document to be redacted
    with Redactor("./annotated.xlsx") as redactor:
        # Apply the redaction
        result = redactor.apply(a_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    remove_all_annotations()
```
{{< /tab >}}
{{< tab "annotated.xlsx" >}}
{{< tab-text >}}
`annotated.xlsx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/annotation-redactions/annotated.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annotated_redacted.xlsx" >}}  
```text
Binary file (XLSX, 12 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/annotation-redactions/remove_all_annotations/annotated_redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}

You can use constructor without arguments to remove all annotations within the document.

## Redact annotations

Instead of removing all or specific annotations, you can remove sensitive data from the annotation text. For instance, we can remove all mentions of "John" in the given document, e.g.:

{{< tabs "code-example-redact-annotations" >}}
{{< tab "redact_annotations.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import AnnotationRedaction


def redact_annotations():
    # Specify the redaction options: search pattern and replacement string
    a_red = AnnotationRedaction("(?im:john)", "[redacted]")

    # Load the document to be redacted
    with Redactor("./annotated.xlsx") as redactor:
        # Apply the redaction
        result = redactor.apply(a_red)

        # Save the redacted document next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    redact_annotations()
```
{{< /tab >}}
{{< tab "annotated.xlsx" >}}
{{< tab-text >}}
`annotated.xlsx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/annotation-redactions/annotated.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "annotated_redacted.xlsx" >}}  
```text
Binary file (XLSX, 12 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/annotation-redactions/redact_annotations/annotated_redacted.xlsx)
{{< /tab >}}
{{< /tabs >}}
