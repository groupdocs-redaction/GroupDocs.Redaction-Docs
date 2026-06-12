---
id: get-supported-file-formats
url: redaction/python-net/get-supported-file-formats
title: Get supported file formats
weight: 1
description: This article shows that how to get the list of all supported file formats of GroupDocs.Redaction by using Python.
keywords: redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction allows to get the list of all supported file formats by these steps:

*   Call [GetSupportedFileTypes](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/get_supported_file_types/) of [FileType](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/) class;
*   Enumerate through the collection of [FileType](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/) objects*.*

The following example demonstrates how to get supported file formats list.

{{< tabs "code-example-list-supported-formats" >}}
{{< tab "list_supported_formats.py" >}}
```python
from groupdocs.redaction import FileType


def list_supported_formats():
    # Retrieve the collection of supported file types
    supported_file_types = FileType.get_supported_file_types()

    # Enumerate the file types sorted by extension
    for file_type in sorted(supported_file_types, key=lambda x: x.extension):
        print(file_type)


if __name__ == "__main__":
    list_supported_formats()
```
{{< /tab >}}
{{< tab "list-supported-formats.txt" >}}  
```text
Bitmap Image File (.bmp)
Comma Separated Values File (.csv)
Microsoft Word Document (.doc)
Word Open XML Macro-Enabled Document (.docm)
Microsoft Word Open XML Document (.docx)
Word Document Template (.dot)
Word Open XML Macro-Enabled Document Template (.dotm)
Word Open XML Document Template (.dotx)
Graphical Interchange Format File (.gif)
Hypertext Markup Language File (.htm)
[TRUNCATED]
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/get-supported-file-formats/list_supported_formats/list-supported-formats.txt)
{{< /tab >}}
{{< /tabs >}}
