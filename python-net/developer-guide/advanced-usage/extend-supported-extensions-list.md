---
id: extend-supported-extensions-list
url: redaction/python-net/extend-supported-extensions-list
title: Extend supported extensions list
weight: 6
description: "This article explains the method which can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured."
keywords: non-standard extensions
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
This method can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured. For instance, all kinds of plain text files (batch, command files, etc.) could be opened. In this case you do not need to create your own format handler. As it is shown below, you can add file extension (e.g. ".dump") as being handled by the same *[DocumentFormatInstance](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.integration/documentformatinstance/)* as all plain text files:

{{< tabs "code-example-extend-supported-extensions-list" >}}
{{< tab "extend_supported_extensions_list.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.configuration import RedactorConfiguration
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def extend_supported_extensions_list():
    # Add the .dump format to the list of supported formats, handled as plain text
    config = RedactorConfiguration.get_instance()

    settings = config.find_format(".txt")

    settings.extension_filter = settings.extension_filter + ",.dump"

    # Specify the redaction options
    repl_opt = ReplacementOptions("[redacted]")
    ex_red = ExactPhraseRedaction("dolor", repl_opt)

    # Load the document with the newly supported extension
    with Redactor("./sample.dump") as redactor:

        # Apply the redaction
        redactor.apply(ex_red)

        # Save the redacted document
        save_options = SaveOptions()
        save_options.add_suffix = True
        save_options.rasterize_to_pdf = True
        save_options.redacted_file_suffix = "redacted"
        result_path = redactor.save(save_options)
        print(f"Document redacted successfully.\nCheck output in {result_path}.")


if __name__ == "__main__":
    extend_supported_extensions_list()
```
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1.9 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/extend-supported-extensions-list/extend_supported_extensions_list/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

In detail, creating your own document format instances is covered in another article.
