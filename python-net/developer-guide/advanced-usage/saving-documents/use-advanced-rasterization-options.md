---
id: use-advanced-rasterization-options
url: redaction/python-net/use-advanced-rasterization-options
title: Use advanced rasterization options
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
## Use advanced rasterization options

In order to use the advanced rasterization options you have to pass one of the options to [Save](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method. In this case the document will be rasterized to PDF, but the scan-like effects will be applied to its pages.

The following example demonstrates how to apply the [AdvancedRasterizationOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/advancedrasterizationoptions/) with default settings. 

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
        
        # Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
        so = gro.SaveOptions()
        so.rasterization.enabled = True
        so.redacted_file_suffix = "_scan"
        so.rasterization.add_advanced_option(gro.AdvancedRasterizationOptions.BORDER)
        so.rasterization.add_advanced_option(gro.AdvancedRasterizationOptions.NOISE)
        so.rasterization.add_advanced_option(gro.AdvancedRasterizationOptions.GRAYSCALE)
        so.rasterization.add_advanced_option(gro.AdvancedRasterizationOptions.TILT)
        redactor.save(so)
```

### Use grayscale rasterization option

The following example demonstrates how to apply the grayscale advanced rasterization option.

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Save the document with the custom grayscale effect
        so = gro.SaveOptions()
        so.rasterization.enabled = True
        so.redacted_file_suffix = "_scan"
        so.rasterization.add_advanced_option(gro.AdvancedRasterizationOptions.GRAYSCALE)
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
