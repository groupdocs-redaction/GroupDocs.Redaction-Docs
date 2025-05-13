---
id: select-specific-pages-for-rasterized-pdf
url: redaction/python-net/select-specific-pages-for-rasterized-pdf
title: Select specific pages for rasterized PDF
weight: 5
description: "This article demonstrates that how you can specify starting page index (zero based) and the number of pages from this index to save a rasterized PDF"
keywords: rasterized PDF
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
Saving document as a rasterized PDF, you can specify starting page index (zero based) and the number of pages from this index to save. Also, you can change the Compliance level from PDF/A-1b, which is used by default, to PDF/A-1a:

**Python**

```python
from operator import truediv
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():

    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions(color)
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        if (result.status != gr.RedactionStatus.FAILED):
            # Save the processed document
            so = gro.SaveOptions()
            so.rasterization.enabled = True # convert pages to images for compatibility
            so.rasterization.page_index = 5 # start from 6th page (index is 0-based)
            so.rasterization.page_count = 1 # save only one page
            so.rasterization.compliance = gro.PdfComplianceLevel.PDF_A1A # PDF format
            so.add_suffix = False
            result_path = redactor.save(so)

            print(f"Document redacted successfully.\nCheck output in {result_path}")
        else:
            print(f"Redaction failed!")
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
   

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
