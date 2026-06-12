---
id: create-pdf-with-image-redaction
url: redaction/python-net/create-pdf-with-image-redaction
title: Create PDF with Image Redaction
weight: 8
description: This article shows how to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text.
keywords: redact
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

In some cases you might need to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text. With GroupDocs.Redaction you can use the following approach:  

*   open the document and apply all required redactions to the document's body (text, annotations, etc.);
*   save it as a rasterized PDF file (containing images of the original document's pages);
*   apply ImageAreaRedaction to remove specific areas on the pages within the PDF document.  
    
The following example demonstrates how to create a rasterized PDF from a Microsoft Word document and apply image redactions to its pages:

{{< tabs "code-example-create-pdf-with-image-redaction" >}}
{{< tab "create_pdf_with_image_redaction.py" >}}
```python
from io import BytesIO

from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import RasterizationOptions
from groupdocs.redaction.redactions import ImageAreaRedaction, RegionReplacementOptions
from groupdocs.pydrawing import Point, Size, Color


def create_pdf_with_image_redaction():
    # Create an in-memory binary stream
    stream = BytesIO()

    # Load the document and rasterize it to a PDF in the stream
    with Redactor("./sample.docx") as redactor:

        # Save the rasterized document to the stream
        ro = RasterizationOptions()
        ro.enabled = True
        redactor.save(stream, ro)
        stream.seek(0)

    # Define the position on the image
    sample_point = Point(40, 160)
    # Define the size of the area which needs to be redacted
    sample_size = Size(350, 75)
    # Define the color of redaction
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = RegionReplacementOptions(color, sample_size)
    img_red = ImageAreaRedaction(sample_point, repl_opt)

    # Load the stream to be redacted
    with Redactor(stream) as redactor:

        # Apply the redaction
        result = redactor.apply(img_red)

        # Re-open the rasterized PDF document to redact its pages as images
        if result.status != RedactionStatus.FAILED:
            # Save the document to a file and convert its pages to images
            ro = RasterizationOptions()
            ro.enabled = True
            with open("./redacted-sample.pdf", "wb") as stream_out:
                redactor.save(stream_out, ro)
            print("Document redacted successfully.\nCheck output in ./redacted-sample.pdf")
        else:
            print("Redaction failed!")


if __name__ == "__main__":
    create_pdf_with_image_redaction()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/create-pdf-with-image-redaction/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "redacted-sample.pdf" >}}  
```text
Binary file (PDF, 879 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/create-pdf-with-image-redaction/create_pdf_with_image_redaction/redacted-sample.pdf)
{{< /tab >}}
{{< /tabs >}}

Please, note that you don't have to use GroupDocs.Redaction to create a rasterized PDF from an office document. You will be able to use it, if you don't have any other tool for that.
