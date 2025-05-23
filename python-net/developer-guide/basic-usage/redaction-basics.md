---
id: redaction-basics
url: redaction/python-net/redaction-basics
title: Redaction basics
weight: 4
description: This article shows that how C# developers can apply metadata, image, annotation and text redaction in their documents. Wide range of document formats is supported, such as, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: text redaction, c#, PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
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
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(ex_red)
        
        if (result.status != gr.RedactionStatus.FAILED):
            # Save the redacted document
            so = gro.SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            result_path = redactor.save(so)
```

All possible statuses of the [RedactionStatus](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionstatus/) enumeration are listed in this table:

| Status | Description | Possible reasons |
| --- | --- | --- |
| *Applied* | Redaction was fully and successfully applied | All operations within redaction process were successfully applied |
| *PartiallyApplied* | Redaction was applied only to a part of its matches | 1) Trial limitations for replacements were exceeded2) At least one change was rejected by user |
| *Skipped* | Redaction was skipped (not applied) | 1) Trial limitations for redactions were exceeded2) Redaction cannot be applied to this type of document3) All replacements were rejected by user and no changes were made |
| *Failed* | Redaction failed with exception | An exception occurred in process of redaction |

For detailed information you have to iterate through redaction log entries in [RedactorChangeLog.RedactionLog](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorchangelog/redaction_log/) and check for [ErrorMessage](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionresult/error_message/) property of any items with status other than *Applied*:

**Python**

```python
result = redactor.apply = redactor.Apply( ... );
if (result.status != gr.RedactionStatus.FAILED):
    # By default, the redacted document is saved in PDF format
    result_path = redactor.save()
    print(f"Document redacted successfully.\nCheck output in {result_path}")
else:
    # Dump all failed or skipped redactions
    print(f"Redaction failed!")
    for log_entry in result.redaction_log:
        if (log_entry.result.status != gr.RedactionStatus.APPLIED):
            print(f"Status is {log_entry.result.status}, details: {log_entry.result.error_message}")
```

## Apply multiple redactions

You can apply as much redactions as you need in a single call to [Redactor.Apply](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactor/apply/) method, since its overload accepts an array of redactions and redaction policy. In this case, redactions will be applied in the same order as they appear in the array. As an alternative to specifying redaction sets in your code, you can create an XML file with redaction policy, as described [here]({{< ref "redaction/python-net/developer-guide/advanced-usage/use-redaction-policies.md" >}}).

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():
    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Provide redaction options
    redactionList = [
        grr.ExactPhraseRedaction("John Doe", grr.ReplacementOptions("[Client]")),
        grr.RegexRedaction("Redaction", grr.ReplacementOptions("[Product]")),
        grr.RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", grr.ReplacementOptions(color)),
        grr.DeleteAnnotationRedaction(),
        grr.EraseMetadataRedaction(grr.MetadataFilters.ALL)
    ]

    # Load the document to be redacted
    with gr.Redactor("source.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(redactionList)

        if (result.status != gr.RedactionStatus.FAILED):
            # By default, the redacted document is saved in PDF format
            result_path = redactor.save()
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
