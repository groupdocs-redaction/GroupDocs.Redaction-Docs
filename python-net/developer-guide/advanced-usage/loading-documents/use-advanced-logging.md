---
id: use-advanced-logging
url: redaction/python-net/use-advanced-logging
title: Use advanced logging
weight: 4
description: "Collect the errors, warnings and trace messages GroupDocs.Redaction for Python via .NET reports while it redacts, with a logger object."
keywords: logging, logger, ILogger, error, warning, trace, RedactorSettings, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction reports what happens during a redaction to a logger, the Python side of the [ILogger](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/ilogger/) interface. A logger is any object with these three methods, each receiving a message:

* `error(message)`: an error that occurred during the redaction;
* `warning(message)`: a warning;
* `trace(message)`: an event, such as a redaction applied.

A method the object lacks is skipped. A function `fn(level, message)` also works as a logger, with `level` being `"error"`, `"warning"` or `"trace"`. A logger that raises is reported on stderr and never stops the redaction.

Pass the logger to [RedactorSettings](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/redactorsettings/), the third argument of `Redactor`:

{{< tabs "code-example-use-advanced-logging" >}}
{{< tab "use_advanced_logging.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import LoadOptions, RedactorSettings
from groupdocs.redaction.redactions import DeleteAnnotationRedaction, ExactPhraseRedaction, ReplacementOptions


class CustomLogger(object):
    """Keeps every message, by level."""

    def __init__(self):
        self.errors = []
        self.warnings = []
        self.traces = []

    def error(self, message):
        self.errors.append(message)

    def warning(self, message):
        self.warnings.append(message)

    def trace(self, message):
        self.traces.append(message)


def use_advanced_logging():
    logger = CustomLogger()
    with Redactor("./sample.docx", LoadOptions(), RedactorSettings(logger)) as redactor:
        redactor.apply(DeleteAnnotationRedaction())
        redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[personal]")))
        for message in logger.traces:
            print("trace: " + message)
        if not logger.errors:
            result_path = redactor.save()
            print("No errors. Output saved to " + result_path)
        else:
            print("Not saved, %d error(s): %s" % (len(logger.errors), logger.errors[0]))


if __name__ == "__main__":
    use_advanced_logging()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/use-advanced-logging/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1.1 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/use-advanced-logging/use_advanced_logging/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
