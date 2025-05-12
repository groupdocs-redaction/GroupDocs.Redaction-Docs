---
id: spreadsheet-redactions
url: redaction/python-net/spreadsheet-redactions
title: Spreadsheet redactions
weight: 8
description: This article shows that how C# redaction API allows to redact data of sensitive or private nature from your XLS, XLSX, ODS spreadsheet document formats and others.
keywords: c#, redaction, redact data, xls, xlsx, ods 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
GroupDocs.Redaction allows to redact data of sensitive or private nature from your XLS, XLSX, ODS spreadsheet document formats and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

## Redact spreadsheet content

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    repl_opt = grr.ReplacementOptions("-redacted-")
    ex_red = grr.ExactPhraseRedaction("John Doe", repl_opt)

    #Load the document to be redacted
    with gr.Redactor("source.xlsx") as redactor:

        #Apply the redaction
        result = redactor.apply(ex_red)

        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/python-net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
