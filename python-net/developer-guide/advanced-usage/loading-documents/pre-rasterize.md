---
id: pre-rasterize
url: redaction/python-net/pre-rasterize
title: Pre-rasterize
weight: 5
description: "This article shows how to pre-rasterize a document using the redaction API."
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
In some cases, you might need to pre-rasterize the document before opening it and applying redactions. 

For instance, you might need to use an [ImageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/imagearearedaction/) for a whole page of a document with search-able text and images. In order to do that, you will need to pass the Boolean flag to the [LoadOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/) class constructor.

The following example demonstrates how to pre-rasterize a Microsoft Word document:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():
    
    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("[personal]")
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)

        if (result.status != gr.RedactionStatus.FAILED):
            # By default, the redacted document is saved in PDF format
            result_path = redactor.save()
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
