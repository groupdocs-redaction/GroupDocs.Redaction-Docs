---
id: select-specific-pages-for-rasterized-pdf
url: redaction/python-net/select-specific-pages-for-rasterized-pdf
title: Select specific pages for rasterized PDF
weight: 5
description: "This article demonstrates that how you can specify starting page index (zero based) and the number of pages from this index to save a rasterized PDF"
keywords: rasterized PDF
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
Saving document as a rasterized PDF, you can specify starting page index (zero based) and the number of pages from this index to save. Also, you can change the Compliance level from PDF/A-1b, which is used by default, to PDF/A-1a:

{{< tabs "code-example-select-specific-pages-for-rasterized-pdf" >}}
{{< tab "select_specific_pages_for_rasterized_pdf.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions, PdfComplianceLevel
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.pydrawing import Color


def select_specific_pages_for_rasterized_pdf():
    # Define the color of redaction
    color = Color.from_argb(255, 220, 20, 60)

    # Specify the redaction options
    repl_opt = ReplacementOptions(color)
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./multipage_sample.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)

        if result.status != RedactionStatus.FAILED:
            # Save the processed document, selecting the page range and compliance level
            so = SaveOptions()
            so.rasterization.enabled = True  # convert pages to images for compatibility
            so.rasterization.page_index = 5  # start from 6th page (index is 0-based)
            so.rasterization.page_count = 1  # save only one page
            so.rasterization.compliance = PdfComplianceLevel.PDF_A1A  # PDF/A-1a format
            so.add_suffix = False
            result_path = redactor.save(so)

            print(f"Document redacted successfully.\nCheck output in {result_path}")
        else:
            print("Redaction failed!")


if __name__ == "__main__":
    select_specific_pages_for_rasterized_pdf()
```
{{< /tab >}}
{{< tab "multipage_sample.docx" >}}
{{< tab-text >}}
`multipage_sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/select-specific-pages-for-rasterized-pdf/multipage_sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}  
```text
Binary file (PDF, 10.8 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/select-specific-pages-for-rasterized-pdf/select_specific_pages_for_rasterized_pdf/multipage_sample.pdf)
{{< /tab >}}
{{< /tabs >}}
