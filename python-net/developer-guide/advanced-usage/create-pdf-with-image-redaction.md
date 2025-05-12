---
id: create-pdf-with-image-redaction
url: redaction/python-net/create-pdf-with-image-redaction
title: Create PDF with Image Redaction
weight: 8
description: This article shows how to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text.
keywords: redact
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---

In some cases you might need to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text. With GroupDocs.Redaction you can use the following approach:  

*   open the document and apply all required redactions to the document's body (text, annotations, etc.);
    
*   save it as a rasterized PDF file (containing images of the original document's pages);
    
*   apply ImageAreaRedaction to remove specific areas on the pages within the PDF document.  
    
The following example demonstrates how to create a rasterized PDF from a Microsoft Word document and apply image redactions to its pages:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.redaction.configuration as grc
import groupdocs.pydrawing as grd
from io import BytesIO
import os

def run():

    # Create an in-memory binary stream
    stream = BytesIO()

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Save the redacted document
        ro = gro.RasterizationOptions()
        ro.enabled = True
        redactor.save(stream, ro)
        stream.seek(0)

    # Define the position on image
    sample_point = grd.Point(40, 160)
    # Define the size of the area which need to be redacted
    sample_size = grd.Size(350, 75)
    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = grr.RegionReplacementOptions(color, sample_size)
    img_red = grr.ImageAreaRedaction(sample_point, repl_opt)

    # Load the stream to be redacted
    with gr.Redactor(stream) as redactor:

        # Apply the redaction
        result = redactor.apply(img_red)
        
        # Re-open the rasterized PDF document to redact its pages as images
        if (result.status != gr.RedactionStatus.FAILED):
            # Save the document to a custom location and convert its pages to images
            ro = gro.RasterizationOptions()
            ro.enabled = True
            with open("output.pdf", "wb") as stream_out:
                redactor.save(stream_out, ro)
```

Please, note that you don't have to use GroupDocs.Redaction to create a rasterized PDF from an office document. You will be able to use it, if you don't have any other tool for that.

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
