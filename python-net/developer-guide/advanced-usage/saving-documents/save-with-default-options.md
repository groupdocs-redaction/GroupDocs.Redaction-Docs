---
id: save-with-default-options
url: redaction/python-net/save-with-default-options
title: Save with default options
weight: 4
description: "This article demonstrates the simplest way to save the document"
keywords: simplest way to save the document
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
The simplest way to save the document is it provide no parameters to [Save](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method. In this case the document will be rasterized to PDF and will have the same name as the original one except its extension (.PDF). The PDF file will be overwritten.

The following example demonstrates usage of [Save()](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method with default options.

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("[personal]")
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        # Save the document with default options (convert pages into images, save as PDF)
        result_path = redactor.save()

    # Indicate the successful rendering of the source document and specify where to find the output in the specified directory
    print(f"Document redacted successfully.\nCheck output in {result_path}.")
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
