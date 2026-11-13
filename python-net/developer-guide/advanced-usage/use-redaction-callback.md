---
id: use-redaction-callback
url: redaction/python-net/use-redaction-callback
title: Use redaction callback
weight: 5
description: "Approve or reject each change GroupDocs.Redaction for Python via .NET proposes, and log every change, with a redaction callback."
keywords: redaction callback, accept_redaction, IRedactionCallback, RedactorSettings, approve changes, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
To approve or reject each change during the redaction process, or to keep a full log of the changes, give [RedactorSettings](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/redactorsettings/) a redaction callback. It is the Python side of the [IRedactionCallback](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/iredactioncallback/) interface: an object with an `accept_redaction(description)` method, or a function that takes `description`. It is called once for each change the engine is about to make, and returns `True` to make the change or `False` to skip it.

`description` is a [RedactionDescription](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/redactiondescription/), valid during the call:

* `redaction_type` and `action_type`: what kind of redaction it is and what it is about to do;
* `original_text`: the matched text;
* `replacement`: for a text replacement, the original and the replacement text;
* `image_area_replacement`: for an image area, the fill options.

## Log every change

The following callback prints each change and accepts it:

{{< tabs "code-example-use-redaction-callback" >}}
{{< tab "use_redaction_callback.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import LoadOptions, RedactorSettings
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


class RedactionDump(object):
    def accept_redaction(self, description):
        print("%s redaction, %s action, item %s." % (
            description.redaction_type.name, description.action_type.name, description.original_text))
        if description.replacement is not None:
            print("Text %s is replaced with %s." % (
                description.replacement.original_text, description.replacement.replacement))
        # Return False here to skip this change
        return True


def use_redaction_callback():
    settings = RedactorSettings(RedactionDump())
    with Redactor("./sample.docx", LoadOptions(), settings) as redactor:
        redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[personal]")))
        result_path = redactor.save()
        print("Document redacted. Output saved to " + result_path)


if __name__ == "__main__":
    use_redaction_callback()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/use-redaction-callback/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 948 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/use-redaction-callback/use_redaction_callback/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

`RedactorSettings` is the third argument of `Redactor`, after the load options.

## Skip some of the changes

A plain function works as well. The one below accepts only the first match. The redaction's entry in the change log then reports `PARTIALLY_APPLIED`, with the reason in its error message:

{{< tabs "code-example-skip-some-changes" >}}
{{< tab "skip_some_changes.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import LoadOptions, RedactorSettings
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def skip_some_changes():
    accepted = []

    def accept_first_only(description):
        accepted.append(description.original_text)
        return len(accepted) == 1

    settings = RedactorSettings(callback=accept_first_only)
    with Redactor("./sample.docx", LoadOptions(), settings) as redactor:
        result = redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[personal]")))
        entry = result.redaction_log[0].result
        print("Matches offered: %d, status: %s (%s)" % (len(accepted), entry.status.name, entry.error_message))
        redactor.save()


if __name__ == "__main__":
    skip_some_changes()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/use-redaction-callback/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 950 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/use-redaction-callback/skip_some_changes/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

An exception raised in the callback does not stop `apply()`: the engine marks that redaction `FAILED`, and the message is in the result's redaction log (`result.redaction_log[i].result.error_message`).
