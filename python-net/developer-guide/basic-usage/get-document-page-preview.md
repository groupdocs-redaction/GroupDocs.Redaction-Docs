---
id: get-document-page-preview
url: redaction/python-net/get-document-page-preview
title: Get document page preview
weight: 3
description: "Render document pages to PNG, JPEG or BMP images with GroupDocs.Redaction for Python via .NET, to files or to memory, before or after redacting."
keywords: page preview, thumbnail, PNG, JPEG, BMP, generate_preview, PreviewOptions, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
[Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/) renders document pages to images in one of these formats:

* Portable Network Graphics (PNG)
* JPEG Image
* Bitmap Image File (BMP)

Pass a [PreviewOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/previewoptions/) to `generate_preview()`. Its first argument is a function that receives a page number and returns a writable binary stream for that page: an open file or an `io.BytesIO`. Set `width`, `height` and `page_numbers`: the engine raises an error when any of them is left unset.

## Save a page preview to a file

The following example renders the first page of a document to a PNG file:

{{< tabs "code-example-get-document-page-preview" >}}
{{< tab "get_document_page_preview.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import PreviewOptions


def get_document_page_preview():
    # Return a writable stream for each page the engine renders
    def create_page_stream(page_number):
        return open("preview_page_%d.png" % page_number, "wb")

    with Redactor("./multipage_sample.docx") as redactor:
        options = PreviewOptions(create_page_stream)
        options.width = 480
        options.height = 640
        options.page_numbers = [1]
        options.preview_format = PreviewOptions.PreviewFormats.PNG
        redactor.generate_preview(options)
        print("The preview of page 1 is saved to preview_page_1.png")


if __name__ == "__main__":
    get_document_page_preview()
```
{{< /tab >}}
{{< tab "multipage_sample.docx" >}}
{{< tab-text >}}
`multipage_sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/get-document-page-preview/multipage_sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "preview_page_1.png" >}}  
```text
Binary file (PNG, 27 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/get-document-page-preview/get_document_page_preview/preview_page_1.png)
{{< /tab >}}
{{< /tabs >}}

The engine closes each stream once it has written the page, so the file is complete when `generate_preview()` returns.

## Render page previews into memory

A second function, passed after the first, is called when a page is done. It receives the page number and the stream the first function returned for it. With an `io.BytesIO`, the page's image is in the buffer by then:

{{< tabs "code-example-get-page-previews-in-memory" >}}
{{< tab "get_page_previews_in_memory.py" >}}
```python
import io

from groupdocs.redaction import Redactor
from groupdocs.redaction.options import PreviewOptions


def get_page_previews_in_memory():
    def create_page_stream(page_number):
        return io.BytesIO()

    def release_page_stream(page_number, stream):
        # The stream is closed and filled: keep, upload or inspect the image
        print("Page %d: %d bytes of JPEG" % (page_number, len(stream.getvalue())))

    with Redactor("./multipage_sample.docx") as redactor:
        options = PreviewOptions(create_page_stream, release_page_stream)
        options.width = 300
        options.height = 400
        options.page_numbers = [1, 2, 3]
        options.preview_format = PreviewOptions.PreviewFormats.JPEG
        redactor.generate_preview(options)


if __name__ == "__main__":
    get_page_previews_in_memory()
```
{{< /tab >}}
{{< tab "multipage_sample.docx" >}}
{{< tab-text >}}
`multipage_sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/get-document-page-preview/multipage_sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-page-previews-in-memory.txt" >}}  
```text
Page 1: 14013 bytes of JPEG
Page 2: 13575 bytes of JPEG
Page 3: 11155 bytes of JPEG
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/get-document-page-preview/get_page_previews_in_memory/get-page-previews-in-memory.txt)
{{< /tab >}}
{{< /tabs >}}

A preview shows the document as it was loaded, without the redactions applied since. To preview the redacted result, save it and open the saved document with a new `Redactor`.
