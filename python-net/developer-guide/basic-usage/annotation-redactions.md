---
id: annotation-redactions
url: redaction/python-net/annotation-redactions
title: Annotation redactions
weight: 7
description: This article shows the implementation of annotation redaction for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others.
keywords: annotation, redactions,PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
With GroupDocs.Redaction API you can apply annotation redactions for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redactions provides a flexible API that allows to remove sensitive data from annotation text, or completely remove annotations by a regular expression.

## Remove annotations (comments etc)

You can use GroupDocs.Redaction to remove all or specific comments and other annotations from the document. For example, we can remove all comments from the document, containing texts like "use", "show" or "describe" in its body:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr

def run():
    # Specify the redaction options
    a_red = grr.DeleteAnnotationRedaction("(?im:(use|show|describe))")

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(a_red)
        
        # Save the redacted document
        redactor.save()
```

You can use constructor without arguments to remove all annotations within the document.

## Redact annotations

Instead of removing all or specific annotations, you can remove sensitive data from the annotation text. For instance, we can remove all mentions of "John" in the given document, e.g.:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr

def run():
    # Specify the redaction options
    a_red = grr.AnnotationRedaction("(?im:john)", "[redacted]")

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(a_red)
        
        # Save the redacted document
        redactor.save()
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
