---
id: image-redactions
url: redaction/python-net/image-redactions
title: Image redactions
weight: 9
description: This article shows that how to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others.
keywords: redact data,JPG, PNG, TIFF
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redactions provides a set of features to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redaction  supports two ways of redacting images, both in separate image files and embedded images:
*   You can put a colored box over a given area, such as header, footer, or an area, where customer's data are expected to appear.
*   You can use any 3-rd party OCR engine to process the image, search it for text and redact sensitive data within the image.   

GroupDocs.Redaction for Python via .NET also allows you to change image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

## Redact image area

In order to redact image area, you have to use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/imagearearedaction/) class:

{{< tabs "code-example-redact-image-area" >}}
{{< tab "redact_image_area.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ImageAreaRedaction, RegionReplacementOptions
from groupdocs.pydrawing import Color, Point, Size


def redact_image_area():
    # Define the top-left position of the area to redact
    sample_point = Point(385, 485)
    # Define the size of the area which needs to be redacted
    sample_size = Size(1793, 2069)
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = RegionReplacementOptions(color, sample_size)
    img_red = ImageAreaRedaction(sample_point, repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.jpg") as redactor:
        # Apply the redaction
        result = redactor.apply(img_red)

        if result.status != RedactionStatus.FAILED:
            # By default, the redacted document is saved in PDF format
            save_options = SaveOptions()
            save_options.add_suffix = True
            save_options.rasterize_to_pdf = True
            save_options.redacted_file_suffix = "redacted"
            redactor.save(save_options)


if __name__ == "__main__":
    redact_image_area()
```
{{< /tab >}}
{{< tab "sample.jpg" >}}
{{< tab-text >}}
`sample.jpg` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/image-redactions/sample.jpg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 2.7 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/image-redactions/redact_image_area/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

If the redaction cannot be applied to this type of files, e.g. MS Word document without embedded images, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Clean image metadata

The following example demonstrates how to edit exif data (erase them) from a photo or any other image:

{{< tabs "code-example-clean-image-metadata" >}}
{{< tab "clean_image_metadata.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import EraseMetadataRedaction, MetadataFilters


def clean_image_metadata():
    # Specify the redaction options to remove all image metadata (e.g. EXIF)
    er_opt = EraseMetadataRedaction(MetadataFilters.ALL)

    # Load the image to be redacted
    with Redactor("./sample.jpg") as redactor:
        # Apply the redaction
        result = redactor.apply(er_opt)

        # Save the redacted image next to the source file
        so = SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        so.redacted_file_suffix = "redacted"
        redactor.save(so)


if __name__ == "__main__":
    clean_image_metadata()
```
{{< /tab >}}
{{< tab "sample.jpg" >}}
{{< tab-text >}}
`sample.jpg` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/image-redactions/sample.jpg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.jpg" >}}  
```text
Binary file (JPG, 3.1 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/image-redactions/clean_image_metadata/sample_redacted.jpg)
{{< /tab >}}
{{< /tabs >}}

If the redaction cannot be applied to this type of files, e.g. BMP image, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Redact embedded images

You can redact image area within all kinds of embedded images inside a document. 

The following example demonstrates how to redact all embedded images within a Microsoft Word document:

{{< tabs "code-example-redact-embedded-images" >}}
{{< tab "redact_embedded_images.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ImageAreaRedaction, RegionReplacementOptions
from groupdocs.pydrawing import Color, Point, Size


def redact_embedded_images():
    # Define the top-left position of the area to redact
    sample_point = Point(516, 311)
    # Define the size of the area which needs to be redacted
    sample_size = Size(170, 35)
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = RegionReplacementOptions(color, sample_size)
    img_red = ImageAreaRedaction(sample_point, repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction to all embedded images
        result = redactor.apply(img_red)

        if result.status != RedactionStatus.FAILED:
            # By default, the redacted document is saved in PDF format
            save_options = SaveOptions()
            save_options.add_suffix = True
            save_options.rasterize_to_pdf = True
            save_options.redacted_file_suffix = "redacted"
            redactor.save(save_options)


if __name__ == "__main__":
    redact_embedded_images()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/image-redactions/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1022 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/image-redactions/redact_embedded_images/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

If the redaction cannot be applied to this type of files, e.g. a spreadsheet document, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Multi-frame images

You can remove frames from a multi-frame image with a given origin and frame count. For additional information look at [remove page redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/remove-page-redactions.md" >}}) article.

Some image formats, such as DjVu documents, require [pre-rasterization]({{< ref "redaction/python-net/developer-guide/advanced-usage/loading-documents/pre-rasterize.md" >}}) and further saving in PDF format.
