---
id: load-from-local-disc
url: redaction/python-net/load-from-local-disc
title: Load from local disc
weight: 1
description: "This article shows how the redaction API is used to load file from disk."
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
[GroupDocs.Redaction.Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/) class is a main class in Redaction API, providing functionality to open a document. When document is located on the local disk, you can pass its path to [Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor)  class constructor.

The following example demonstrates how to open a document from local disc:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options - remove all annotations
    del_red = grr.DeleteAnnotationRedaction()

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(del_red)
        
        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
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
