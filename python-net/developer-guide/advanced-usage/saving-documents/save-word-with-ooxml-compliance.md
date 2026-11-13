---
id: save-word-with-ooxml-compliance
url: redaction/python-net/save-word-with-ooxml-compliance
title: Save Word with OOXML compliance
weight: 8
description: "Save a redacted Word document in its original format with a chosen OOXML compliance level (Ecma, Transitional or Strict) with GroupDocs.Redaction for Python via .NET."
keywords: OOXML compliance, Strict, Transitional, Ecma, WordprocessingSaveOptions, DOCX, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
When you save a Word document in its original format, you can set its OOXML compliance level through `save_options.wordprocessing_save_options.ooxml_compliance` ([WordprocessingSaveOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/wordprocessingsaveoptions/)). The values come from [WordProcessingComplianceLevel](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/wordprocessingcompliancelevel/): `ECMA`, `TRANSITIONAL` or `STRICT`.

Without it, the compliance level of the original document is kept. A Strict document can be saved as Transitional, but not as Ecma.

The option applies to the OOXML Word formats: DOCX, DOCM, DOTX and DOTM. Set `rasterize_to_pdf` to `False`, so that the document is saved in its Word format instead of as a rasterized PDF.

{{< tabs "code-example-save-word-with-ooxml-compliance" >}}
{{< tab "save_word_with_ooxml_compliance.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions, WordProcessingComplianceLevel
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def save_word_with_ooxml_compliance():
    with Redactor("./sample.docx") as redactor:
        redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[personal]")))

        options = SaveOptions()
        options.add_suffix = True
        options.rasterize_to_pdf = False  # keep the Word format
        options.redacted_file_suffix = "Strict"
        # Without this line the original document's compliance level is kept
        options.wordprocessing_save_options.ooxml_compliance = WordProcessingComplianceLevel.STRICT

        result_path = redactor.save(options)
        print("Output saved to " + result_path)


if __name__ == "__main__":
    save_word_with_ooxml_compliance()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/saving-documents/save-word-with-ooxml-compliance/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Strict.docx" >}}  
```text
Binary file (DOCX, 42 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/saving-documents/save-word-with-ooxml-compliance/save_word_with_ooxml_compliance/sample_Strict.docx)
{{< /tab >}}
{{< /tabs >}}
