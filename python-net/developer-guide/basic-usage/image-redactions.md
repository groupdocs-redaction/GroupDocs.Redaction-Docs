---
id: image-redactions
url: redaction/python-net/image-redactions
title: Image redactions
weight: 9
description: This article shows that how to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others.
keywords: redact data,JPG, PNG, TIFF
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
GroupDocs.Redactions provides a set of features to redact data of sensitive nature from images of various formats like JPG, PNG, TIFF and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redaction  supports two ways of redacting images, both in separate image files and embedded images:
*   You can put a colored box over a given area, such as header, footer, or an area, where customer's data are expected to appear.
*   You can use any 3-rd party OCR engine to process the image, search it for text and redact sensitive data within the image.   

GroupDocs.Redaction for Python via .NET also allows you to change image metadata (e.g. edit EXIF data of an image or act as an "EXIF eraser").

## Redact image area

In order to redact image area, you have to use [ImageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/imagearearedaction/) class:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():

    # Define the position on image
    sample_point = grd.Point(385, 485)
    # Define the size of the area which need to be redacted
    sample_size = grd.Size(1793, 2069)
    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = grr.RegionReplacementOptions(color, sample_size)
    img_red = grr.ImageAreaRedaction(sample_point, repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.jpg") as redactor:

        # Apply the redaction
        result = redactor.apply(img_red)

        if (result.status != gr.RedactionStatus.FAILED):
            # By default, the redacted document is saved in PDF format
            result_path = redactor.save()
```

If the redaction cannot be applied to this type of files, e.g. MS Word document without embedded images, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Clean image metadata

The following example demonstrates how to edit exif data (erase them) from a photo or any other image:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():
    
    print("\n[Example Basic Usage] # clean_image_metadada.py : Clean all image metadata")

    # Specify the redaction options to remove all metadata
    er_opt = grr.EraseMetadataRedaction(grr.MetadataFilters.ALL)

    # Load the document to be redacted
    with gr.Redactor("source.jpg") as redactor:

        # Apply the redaction
        result = redactor.apply(er_opt)

        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
```

If the redaction cannot be applied to this type of files, e.g. BMP image, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Redact embedded images

You can redact image area within all kinds of embedded images inside a document. 

The following example demonstrates how to redact all embedded images within a Microsoft Word document:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():
    # Define the position on image
    sample_point = grd.Point(516, 311)
    # Define the size of the area which need to be redacted
    sample_size = grd.Size(170, 35)
    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = grr.RegionReplacementOptions(color, sample_size)
    img_red = grr.ImageAreaRedaction(sample_point, repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(img_red)

        if (result.status != gr.RedactionStatus.FAILED):
            # By default, the redacted document is saved in PDF format
            result_path = redactor.save()
```

If the redaction cannot be applied to this type of files, e.g. a spreadsheet document, [RedactorChangeLog.Status](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/status/) will be [RedactionStatus.Skipped](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/).

## Multi-frame images

You can remove frames from a multi-frame image with a given origin and frame count. For additional information look at [remove page redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/remove-page-redactions.md" >}}) article.

Some image formats, such as DjVu documents, require [pre-rasterization]({{< ref "redaction/python-net/developer-guide/advanced-usage/loading-documents/pre-rasterize.md" >}}) and further saving in PDF format. 

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/python-net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
