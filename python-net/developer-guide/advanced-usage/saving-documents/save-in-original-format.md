---
id: save-in-original-format
url: redaction/python-net/save-in-original-format
title: Save in original format
weight: 1
description: "This article demonstrates that how to save file in its original format with current date as a suffix"
keywords: save file in its original format
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
The following example demonstrates how to save file in its original format with current date as a suffix:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
from datetime import datetime

def run():

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("[personal]")
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        date_time_str = datetime.now().strftime("%Y-%m-%d %H-%M-%S")
        so.redacted_file_suffix = date_time_str

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
