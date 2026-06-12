---
id: remove-page-redactions
url: redaction/python-net/remove-page-redactions
title: Remove page redactions
weight: 10
description: This article shows that how to remove pages with sensitive data from your PDF, presentation and spreadsheet documents.
keywords: remove page,PDF,Excel,PowerPoint,spreadsheet,presentation
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Redaction allows to easily to remove pages from PDF documents, slides from presentations and worksheets from spreadsheet documents. 

With GroupDocs.Redaction API you can remove pages by specifying the page range by means of its relative position (the beginning or the end), zero-based index and the count of pages to remove. At this time the supported formats are: PDF, presentations (Microsoft PowerPoint, OpenOffice Presentations), word processing documents (Microsoft Word, OpenOffice Texts, Rich Text Files), spreadsheets (Microsoft Excel, OpenOffice Spreadsheets, etc.) and multi-frame images.

## Remove page range

In the example below, we remove 2nd, 3rd and 4th pages from the document, if the document has enough pages:

{{< tabs "code-example-remove-page-range" >}}
{{< tab "remove_page_range.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import RemovePageRedaction, PageSeekOrigin


def remove_page_range():
    # Load the document to be redacted
    with Redactor("./multipage_sample.pdf") as redactor:
        # Get document info
        doc_info = redactor.get_document_info()

        # Requires at least 4 pages
        if doc_info.page_count > 3:
            # Remove 3 pages starting from the 2nd one (zero-based index 1)
            rem_opt = RemovePageRedaction(PageSeekOrigin.BEGIN, 1, 3)

            # Apply the redaction
            result = redactor.apply(rem_opt)

            # Save the redacted document next to the source file
            so = SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            so.redacted_file_suffix = "redacted"
            redactor.save(so)


if __name__ == "__main__":
    remove_page_range()
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/remove-page-redactions/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

## Remove last page

In some cases you might need to delete the last page or a number of pages, no matter how many pages are there.

The following example demonstrates how to remove the last page from a document:

{{< tabs "code-example-remove-last-page" >}}
{{< tab "remove_last_page.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import RemovePageRedaction, PageSeekOrigin


def remove_last_page():
    # Remove 1 page counting from the end of the document
    rem_opt = RemovePageRedaction(PageSeekOrigin.END, 0, 1)

    # Load the document to be redacted
    with Redactor("./multipage_sample.pdf") as redactor:
        # Get document info
        doc_info = redactor.get_document_info()

        # Requires at least 2 pages so the document is not left empty
        if doc_info.page_count > 1:
            # Apply the redaction
            result = redactor.apply(rem_opt)

            # Save the redacted document next to the source file
            so = SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            so.redacted_file_suffix = "redacted"
            redactor.save(so)


if __name__ == "__main__":
    remove_last_page()
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/remove-page-redactions/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multipage_sample_redacted.pdf" >}}  
```text
Binary file (PDF, 190 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/remove-page-redactions/remove_last_page/multipage_sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

## Remove frame from image

In case of a multi-frame image you might need to delete a number of frames (treated as "pages").

The following example demonstrates how to remove 3 frames from an animated GIF image:

{{< tabs "code-example-remove-frame-from-image" >}}
{{< tab "remove_frame_from_image.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import RemovePageRedaction, PageSeekOrigin


def remove_frame_from_image():
    # Remove frames starting from the 3rd one (zero-based index 2)
    rem_opt = RemovePageRedaction(PageSeekOrigin.BEGIN, 2, 5)

    # Load the multi-frame image to be redacted
    with Redactor("./sample.gif") as redactor:
        # Get document info
        doc_info = redactor.get_document_info()

        # Requires at least 7 frames
        if doc_info.page_count >= 7:
            # Apply the redaction
            result = redactor.apply(rem_opt)

            # Save the redacted image next to the source file
            so = SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            so.redacted_file_suffix = "redacted"
            redactor.save(so)


if __name__ == "__main__":
    remove_frame_from_image()
```
{{< /tab >}}
{{< tab "sample.gif" >}}
{{< tab-text >}}
`sample.gif` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/remove-page-redactions/sample.gif) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.gif" >}}  
```text
Binary file (GIF, 704 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/remove-page-redactions/remove_frame_from_image/sample_redacted.gif)
{{< /tab >}}
{{< /tabs >}}
