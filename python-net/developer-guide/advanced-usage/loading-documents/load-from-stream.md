---
id: load-from-stream
url: redaction/python-net/load-from-stream
title: Load from Stream
weight: 2
description: "This article shows that how to load file from stream using redaction API"
keywords: redaction API
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
As an alternative to a local file, [Redactor](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/) can open a document from stream.

The following example demonstrates how to load and redact a document using Stream:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options - remove all annotations
    del_red = grr.DeleteAnnotationRedaction()

    # Load the document as stream to be redacted
    with open("source.docx", "rb") as stream_in:
        with gr.Redactor(stream_in) as redactor:

            # Apply the redaction
            result = redactor.apply(del_red)
        
            # Save the redacted document as PDF
            with open("output.pdf", "wb") as stream_out:
                ro = gro.RasterizationOptions()
                redactor.save(stream_out, ro)
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
