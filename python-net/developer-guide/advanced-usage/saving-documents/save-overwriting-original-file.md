---
id: save-overwriting-original-file
url: redaction/python-net/save-overwriting-original-file
title: Save overwriting original file
weight: 3
description: "This article demonstrates that how to save the redacted document, replacing an original file"
keywords: save the redacted document, redacted document
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
The following example demonstrates how to save the redacted document, replacing an original file:

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
            # Save the redacted document
            so = gro.SaveOptions()
            so.add_suffix = False
            so.rasterize_to_pdf = False
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
