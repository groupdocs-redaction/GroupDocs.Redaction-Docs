---
id: extend-supported-extensions-list
url: redaction/python-net/extend-supported-extensions-list
title: Extend supported extensions list
weight: 6
description: "This article explains the method which can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured."
keywords: non-standard extensions
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
This method can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured. For instance, all kinds of plain text files (batch, command files, etc.) could be opened. In this case you do not need to create your own format handler. As it is shown below, you can add file extension (e.g. ".dump") as being handled by the same *[DocumentFormatInstance](https://reference.groupdocs.com/python-net/redaction/groupdocs.redaction.integration/documentformatinstance)* as all plain text files:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.redaction.configuration as grc

def run():

    # Add .dump format to the list of supported formats
    config = grc.RedactorConfiguration.get_instance()

    settings = config.find_format(".txt")

    settings.extension_filter = settings.extension_filter + ",.dump";

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("[redacted]")
    ex_red = grr.ExactPhraseRedaction("dolor", repl_opt)

    # Load the document to be redacted
    with gr.Redactor("source.dump") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        # Save the redacted document
        redactor.save()
```

In detail, creating your own document format instances is covered in another article.

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
