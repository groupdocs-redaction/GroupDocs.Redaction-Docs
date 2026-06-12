---
id: get-file-info
url: redaction/python-net/get-file-info
title: Get file info
weight: 2
description: This article explains the ability of the GroupDocs.Redaction API to get the general document information, which includes FileType, PageCount and FileSize.
keywords: redaction, FileType, PageCount, FileSize
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction provides general document information, which includes:

*   FileType
*   PageCount
*   FileSize

The following code examples demonstrate how to get document information.

## Get file info for a file from local disk

{{< tabs "code-example-get-local-file-info" >}}
{{< tab "get_local_file_info.py" >}}
```python
from groupdocs.redaction import Redactor


def get_local_file_info():
    # Load the document from local disk
    with Redactor("./sample.docx") as redactor:
        # Retrieve general document information
        info = redactor.get_document_info()

        print(f"File type: {info.file_type}")
        print(f"Number of pages: {info.page_count}")
        print(f"Document size: {info.size} bytes")


if __name__ == "__main__":
    get_local_file_info()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/get-file-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-local-file-info.txt" >}}  
```text
File type: Microsoft Word Open XML Document (.docx)
Number of pages: 1
Document size: 19370 bytes
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/get-file-info/get_local_file_info/get-local-file-info.txt)
{{< /tab >}}
{{< /tabs >}}

## Get file info for a file from Stream

{{< tabs "code-example-get-file-info-from-stream" >}}
{{< tab "get_file_info_from_stream.py" >}}
```python
from groupdocs.redaction import Redactor


def get_file_info_from_stream():
    # Open the document as a binary stream
    with open("./sample.docx", "rb") as stream:
        # Load the document from the stream
        with Redactor(stream) as redactor:
            # Retrieve general document information
            info = redactor.get_document_info()

            print(f"File type: {info.file_type}")
            print(f"Number of pages: {info.page_count}")
            print(f"Document size: {info.size} bytes")


if __name__ == "__main__":
    get_file_info_from_stream()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/basic-usage/get-file-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-file-info-from-stream.txt" >}}  
```text
File type: Microsoft Word Open XML Document (.docx)
Number of pages: 1
Document size: 19370 bytes
```
[Download full output](/redaction/python-net/_output_files/developer-guide/basic-usage/get-file-info/get_file_info_from_stream/get-file-info-from-stream.txt)
{{< /tab >}}
{{< /tabs >}}
