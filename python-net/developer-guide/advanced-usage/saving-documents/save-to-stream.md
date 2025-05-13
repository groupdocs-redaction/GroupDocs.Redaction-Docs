---
id: save-to-stream
url: redaction/python-net/save-to-stream
title: Save to Stream
weight: 6
description: "This article demonstrates that how to save a document to any custom file at any location on the local disc or a even a Stream"
keywords: save a document to any custom file
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
You might need to save a document to any custom file at any location on the local disc or a even a Stream.

The following example demonstrates how to save a document to any location.

**Python**

```python
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
            # Save the document to a custom location and convert its pages to images
            ro = gro.RasterizationOptions()
            ro.enabled = True
            with open(output_file, "wb") as stream_out:
                redactor.save(stream_out, ro)

            print(f"Document redacted successfully.\nCheck output in {source_file}")
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
