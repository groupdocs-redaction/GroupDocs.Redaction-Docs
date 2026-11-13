---
id: load-with-file-type
url: redaction/python-net/load-with-file-type
title: Load with file type
weight: 6
description: "Open a document from a stream, or a file whose extension does not match its format, by naming its file type in LoadOptions with GroupDocs.Redaction for Python via .NET."
keywords: load options, file type, stream, LoadOptions, FileType, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
When you open a document from a [stream]({{< ref "redaction/python-net/developer-guide/advanced-usage/loading-documents/load-from-stream.md" >}}), or when a file's extension does not match its actual format, pass the format through [LoadOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/loadoptions/). GroupDocs.Redaction then skips format detection and opens the document as the type you name.

Use a constant of the [FileType](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/) class, such as `FileType.DOCX` or `FileType.PDF`: `LoadOptions(FileType.DOCX)`, or `load_options.file_type = FileType.DOCX`. Without it, the format is detected as before.

## Open a stream as a given type

{{< tabs "code-example-load-stream-with-file-type" >}}
{{< tab "load_stream_with_file_type.py" >}}
```python
from groupdocs.redaction import FileType, Redactor
from groupdocs.redaction.options import LoadOptions, SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def load_stream_with_file_type():
    with open("./sample.docx", "rb") as stream_in:
        with Redactor(stream_in, LoadOptions(FileType.DOCX)) as redactor:
            redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[personal]")))

            # Save in the original format, to another stream
            options = SaveOptions()
            options.rasterize_to_pdf = False
            with open("./sample_redacted.docx", "wb") as stream_out:
                redactor.save(stream_out, options)
    print("Output saved to sample_redacted.docx")


if __name__ == "__main__":
    load_stream_with_file_type()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/load-with-file-type/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 40 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/load-with-file-type/load_stream_with_file_type/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

## Open a file whose extension is not its format

{{< tabs "code-example-load-file-with-file-type" >}}
{{< tab "load_file_with_file_type.py" >}}
```python
from groupdocs.redaction import FileType, Redactor
from groupdocs.redaction.options import LoadOptions
from groupdocs.redaction.options.drawing import Color
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


def load_file_with_file_type():
    # The file is a PDF, saved with a .bin extension
    with Redactor("./sample.bin", LoadOptions(FileType.PDF)) as redactor:
        redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions(Color.chocolate)))
        result_path = redactor.save()
        print("Output saved to " + result_path)


if __name__ == "__main__":
    load_file_with_file_type()
```
{{< /tab >}}
{{< tab "sample.bin" >}}
{{< tab-text >}}
`sample.bin` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/loading-documents/load-with-file-type/sample.bin) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 914 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/loading-documents/load-with-file-type/load_file_with_file_type/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
