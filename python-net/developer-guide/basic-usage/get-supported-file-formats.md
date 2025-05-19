---
id: get-supported-file-formats
url: redaction/python-net/get-supported-file-formats
title: Get supported file formats
weight: 1
description: This article shows that how to get the list of all supported file formats of GroupDocs.Redaction by using C#.
keywords: C#, redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
GroupDocs.Redaction allows to get the list of all supported file formats by these steps:

*   Call [GetSupportedFileTypes](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/get_supported_file_types/) of [FileType](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/) class;
*   Enumerate through the collection of [FileType](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/filetype/) objects*.*

The following example demonstrates how to get supported file formats list.

```python
import groupdocs.redaction as gr

def run():

    supported_file_types = gr.FileType.get_supported_file_types()

    for file_type in sorted(supported_file_types, key=lambda x: x.extension):
        print(file_type);
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
