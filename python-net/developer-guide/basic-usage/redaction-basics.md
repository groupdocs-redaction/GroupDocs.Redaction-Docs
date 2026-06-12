---
id: redaction-basics
url: redaction/python-net/redaction-basics
title: Redaction basics
weight: 4
description: This article shows that how Python developers can apply metadata, image, annotation and text redaction in their documents. Wide range of document formats is supported, such as, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: text redaction, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction supports an effective set of document redaction features. It allows to apply redactions for [text]({{< ref "redaction/python-net/developer-guide/basic-usage/text-redactions.md" >}}), [metadata]({{< ref "redaction/python-net/developer-guide/basic-usage/metadata-redactions.md" >}}), [annotations]({{< ref "redaction/python-net/developer-guide/basic-usage/annotation-redactions.md" >}}), [images]({{< ref "redaction/python-net/developer-guide/basic-usage/image-redactions.md" >}}).

Wide range of document formats is supported, such as: PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list of supported formats at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article

## Redaction types

GroupDocs.Redaction comes with the following redaction types:

| Type | Description | Classes |
| --- | --- | --- |
| [Text]({{< ref "redaction/python-net/developer-guide/basic-usage/text-redactions.md" >}}) | Replaces or hides with color block a portion of text within document body | [ExactPhraseRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/exactphraseredaction/), [RegexRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/regexredaction/) |
| [Metadata]({{< ref "redaction/python-net/developer-guide/basic-usage/metadata-redactions.md" >}}) | Replace metadata values with empty ones or redacts metadata texts | [EraseMetadataRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/erasemetadataredaction/), [MetadataSearchRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatasearchredaction/) |
| [Annotations]({{< ref "redaction/python-net/developer-guide/basic-usage/annotation-redactions.md" >}}) | Deletes annotations from document or redacts its texts | [DeleteAnnotationRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/deleteannotationredaction/), [AnnotationRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/annotationredaction/) |
| [Images]({{< ref "redaction/python-net/developer-guide/basic-usage/image-redactions.md" >}}) | Replaces specific area of an image with a colored box | [ImageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/imagearearedaction/) |
| [Pages]({{< ref "redaction/python-net/developer-guide/basic-usage/remove-page-redactions.md" >}}) | Removes specific range of pages (slides, worksheets, etc.) | [RemovePageRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/removepageredaction/) |

## Apply redaction

Applying redaction to a document is done through [Redactor.Apply](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/apply/) method. As a result, you receive [RedactorChangeLog](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/) instance, containing a log entry for each redaction applied. The entry contains reference to [Redacton](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redaction/) instance including its options, status of the operation (see below) and textual descriptions when applicable. If at least one redaction failed, you will see [Status == RedactionStatus.Failed](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/):

{{< tabs "code-example-apply-redaction" >}}
{{< tab "apply_redaction.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def apply_redaction():
    # Specify the redaction options
    repl_opt = ReplacementOptions("[personal]")
    ex_red = ExactPhraseRedaction("John Doe", repl_opt)

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the redaction
        result = redactor.apply(ex_red)

        if result.status != RedactionStatus.FAILED:
            # Save the redacted document next to the source file
            so = SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            so.redacted_file_suffix = "redacted"
            redactor.save(so)


if __name__ == "__main__":
    apply_redaction()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/redaction-basics/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/redaction-basics/apply_redaction/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

All possible statuses of the [RedactionStatus](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/) enumeration are listed in this table:

| Status | Description | Possible reasons |
| --- | --- | --- |
| *Applied* | Redaction was fully and successfully applied | All operations within redaction process were successfully applied |
| *PartiallyApplied* | Redaction was applied only to a part of its matches | 1) Trial limitations for replacements were exceeded2) At least one change was rejected by user |
| *Skipped* | Redaction was skipped (not applied) | 1) Trial limitations for redactions were exceeded2) Redaction cannot be applied to this type of document3) All replacements were rejected by user and no changes were made |
| *Failed* | Redaction failed with exception | An exception occurred in process of redaction |

For detailed information you have to iterate through redaction log entries in [RedactorChangeLog.RedactionLog](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/redaction_log/) and check for [ErrorMessage](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionresult/error_message/) property of any items with status other than *Applied*:

```python
result = redactor.apply(redaction)
if result.status != RedactionStatus.FAILED:
    # By default, the redacted document is saved in PDF format
    save_options = SaveOptions()
    save_options.add_suffix = True
    save_options.rasterize_to_pdf = True
    save_options.redacted_file_suffix = "redacted"
    result_path = redactor.save(save_options)
    print(f"Document redacted successfully.\nCheck output in {result_path}")
else:
    # Dump all failed or skipped redactions
    print("Redaction failed!")
    for log_entry in result.redaction_log:
        if log_entry.result.status != RedactionStatus.APPLIED:
            print(f"Status is {log_entry.result.status}, details: {log_entry.result.error_message}")
```

## Apply multiple redactions

You can apply as much redactions as you need in a single call to [Redactor.Apply](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/apply/) method, since its overload accepts an array of redactions and redaction policy. In this case, redactions will be applied in the same order as they appear in the array. As an alternative to specifying redaction sets in your code, you can create an XML file with redaction policy, as described [here]({{< ref "redaction/python-net/developer-guide/advanced-usage/use-redaction-policies.md" >}}).

{{< tabs "code-example-apply-multiple-redactions" >}}
{{< tab "apply_multiple_redactions.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import (
    ExactPhraseRedaction,
    RegexRedaction,
    ReplacementOptions,
    DeleteAnnotationRedaction,
    EraseMetadataRedaction,
    MetadataFilters,
)
from groupdocs.pydrawing import Color


def apply_multiple_redactions():
    # Define the color of the redaction box
    color = Color.from_argb(255, 220, 20, 60)

    # Provide a list of redactions to apply in order
    redaction_list = [
        ExactPhraseRedaction("John Doe", ReplacementOptions("[Client]")),
        RegexRedaction("Redaction", ReplacementOptions("[Product]")),
        RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", ReplacementOptions(color)),
        DeleteAnnotationRedaction(),
        EraseMetadataRedaction(MetadataFilters.ALL),
    ]

    # Load the document to be redacted
    with Redactor("./sample.docx") as redactor:
        # Apply the list of redactions
        result = redactor.apply(redaction_list)

        if result.status != RedactionStatus.FAILED:
            # By default, the redacted document is saved in PDF format
            save_options = SaveOptions()
            save_options.add_suffix = True
            save_options.rasterize_to_pdf = True
            save_options.redacted_file_suffix = "redacted"
            redactor.save(save_options)
        else:
            # Dump all failed or skipped redactions
            print("Redaction failed!")
            for log_entry in result.redaction_log:
                if log_entry.result.status != RedactionStatus.APPLIED:
                    print(f"Status is {log_entry.result.status}, details: {log_entry.result.error_message}")


if __name__ == "__main__":
    apply_multiple_redactions()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/redaction-basics/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1.2 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/redaction-basics/apply_multiple_redactions/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
