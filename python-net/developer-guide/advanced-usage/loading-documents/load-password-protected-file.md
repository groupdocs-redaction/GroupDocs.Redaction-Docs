---
id: load-password-protected-file
url: redaction/python-net/load-password-protected-file
title: Load password-protected file
weight: 3
description: "Learn how to load a password-protected file by using .NET redaction API"
keywords: redaction API, load a password-protected file
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
In order to open password-protected documents, you have to pass your password to [LoadOptions](https://reference.groupdocs.com/python-net/redaction/groupdocs.redaction.options/loadoptions) class constructor or assign it to its [Password](https://reference.groupdocs.com/python-net/redaction/groupdocs.redaction.options/loadoptions/properties/password) property of an instance of [LoadOptions](https://reference.groupdocs.com/python-net/redaction/groupdocs.redaction.options/loadoptions) class:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr

def run():

    # Specify the load options with document password
    load_opt = gro.LoadOptions("mypassword")

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("[personal]")
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("protected_docx", load_opt) as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        # Save the redacted document
        redactor.save()
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
