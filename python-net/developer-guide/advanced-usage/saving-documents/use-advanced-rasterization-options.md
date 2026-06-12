---
id: use-advanced-rasterization-options
url: redaction/python-net/use-advanced-rasterization-options
title: Use advanced rasterization options
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
## Use advanced rasterization options

In order to use the advanced rasterization options you have to pass one of the options to [Save](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/save/) method. In this case the document will be rasterized to PDF, but the scan-like effects will be applied to its pages.

The following example demonstrates how to apply the [AdvancedRasterizationOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/advancedrasterizationoptions/) with default settings. 

{{< tabs "code-example-use-advanced-rasterization-options" >}}
{{< tab "use_advanced_rasterization_options.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions, AdvancedRasterizationOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def use_advanced_rasterization_options():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
        so = SaveOptions()
        so.rasterization.enabled = True
        so.redacted_file_suffix = "_scan"
        so.rasterization.add_advanced_option(AdvancedRasterizationOptions.BORDER)
        so.rasterization.add_advanced_option(AdvancedRasterizationOptions.NOISE)
        so.rasterization.add_advanced_option(AdvancedRasterizationOptions.GRAYSCALE)
        so.rasterization.add_advanced_option(AdvancedRasterizationOptions.TILT)
        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}")


if __name__ == "__main__":
    use_advanced_rasterization_options()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/use_advanced_rasterization_options/sample.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use grayscale rasterization option

The following example demonstrates how to apply the grayscale advanced rasterization option.

{{< tabs "code-example-use-grayscale-rasterization-option" >}}
{{< tab "use_grayscale_rasterization_option.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions, AdvancedRasterizationOptions


def use_grayscale_rasterization_option():
    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:

        # Save the document with the custom grayscale effect
        so = SaveOptions()
        so.rasterization.enabled = True
        so.redacted_file_suffix = "_scan"
        so.rasterization.add_advanced_option(AdvancedRasterizationOptions.GRAYSCALE)
        result_path = redactor.save(so)
        print(f"Document redacted successfully.\nCheck output in {result_path}")


if __name__ == "__main__":
    use_grayscale_rasterization_option()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.pdf" >}}  
```text
Binary file (PDF, 979 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/use_grayscale_rasterization_option/sample.pdf)
{{< /tab >}}
{{< /tabs >}}
