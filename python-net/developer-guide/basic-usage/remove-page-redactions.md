---
id: remove-page-redactions
url: redaction/python-net/remove-page-redactions
title: Remove page redactions
weight: 10
description: This article shows that how to remove pages with sensitive data from your PDF, presentation and spreadsheet documents.
keywords: remove page,PDF,Excel,PowerPoint,spreadsheet,presentation
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---

GroupDocs.Redaction allows to easily to remove pages from PDF documents, slides from presentations and worksheets from spreadsheet documents. 

With GroupDocs.Redaction API you can remove pages by specifying the page range by means of its relative position (the beginning or the end), zero-based index and the count of pages to remove. At this time the supported formats are: PDF, presentations (Microsoft PowerPoint, OpenOffice Presentations), word processing documents (Microsoft Word, OpenOffice Texts, Rich Text Files), spreadsheets (Microsoft Excel, OpenOffice Spreadsheets, etc.) and multi-frame images.

## Remove page range

In the example below, we remove 2nd, 3rd and 4th pages from the document, if the document has enough pages:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr

def run():
    
    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:
        
        # Get document info
        doc_info = redactor.get_document_info()

        # Requires at least 4 pages
        if doc_info.page_count > 3:

            # Remove 3 pages starting from 2nd one, requires at least 4 pages
            rem_opt = grr.RemovePageRedaction(grr.PageSeekOrigin.BEGIN, 1, 3)
    
            # Apply the redaction
                result = redactor.apply(rem_opt)
        
                # Save the redacted document
                 redactor.save()
```

## Remove last page

In some cases you might need to delete the last page or a number of pages, no matter how many pages are there.

The following example demonstrates how to remove the last page from a document:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr

def run():
    
    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:
        
        # Get document info
        doc_info = redactor.get_document_info()

        # Requires at least 1 page
        if doc_info.page_count > 0:

            rem_opt = grr.RemovePageRedaction(grr.PageSeekOrigin.END, 0, 1)
    
            # Apply the redaction
                result = redactor.apply(rem_opt)
        
                # Save the redacted document
                 redactor.save()
```

## Remove frame from image

In case of a multi-frame image you might need to delete a number of frames (treated as "pages").

The following example demonstrates how to remove 3 frames from an animated GIF image:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    rem_opt = grr.RemovePageRedaction(grr.PageSeekOrigin.BEGIN, 2, 5)

    # Load the document to be redacted
    with gr.Redactor("sample.gif") as redactor:

        # Remove 3 frames starting from 3nd one, requires at least 7 frames
        doc_info = redactor.get_document_info()

        if doc_info.page_count >= 7:
            # Apply the redaction
            result = redactor.apply(rem_opt)
        
            # Save the redacted document
            so = gro.SaveOptions()
            so.add_suffix = True
            so.rasterize_to_pdf = False
            result_path = redactor.save(so)
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/python-net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
