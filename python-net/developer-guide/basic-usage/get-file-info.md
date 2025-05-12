---
id: get-file-info
url: redaction/python-net/get-file-info
title: Get file info
weight: 2
description: This article explains the ability of the GroupDocs.Redaction API to get the general document information, which includes FileType, PageCount and FileSize.
keywords: redaction, c#, FileType, PageCount, FileSize
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
GroupDocs.Redaction provides general document information, which includes:

*   FileType
*   PageCount
*   FileSize

The following code examples demonstrate how to get document information.

## Get file info for a file from local disk

```python
import groupdocs.redaction as gr

def run():
    with gr.Redactor("source.docx") as redactor:
        info = redactor.get_document_info()

        print(f"File type: {info.file_type}")
        print(f"Number of pages: {info.page_count}")
        print(f"Document size: {info.size} bytes")
```

## Get file info for a file from Stream

```python
import groupdocs.redaction as gr

def run():
    with open("source.docx", "rb") as stream:
        with gr.Redactor(stream) as redactor:
            info = redactor.get_document_info()

            print(f"File type: {info.file_type}")
            print(f"Number of pages: {info.page_count}")
            print(f"Document size: {info.size} bytes")
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
