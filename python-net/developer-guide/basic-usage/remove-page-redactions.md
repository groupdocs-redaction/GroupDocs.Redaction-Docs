---
id: remove-page-redactions
url: redaction/net/remove-page-redactions
title: Remove page redactions
weight: 10
description: This article shows that how to remove pages with sensitive data from your PDF, presentation and spreadsheet documents.
keywords: remove page,PDF,Excel,PowerPoint,spreadsheet,presentation
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

GroupDocs.Redaction allows to easily to remove pages from PDF documents, slides from presentations and worksheets from spreadsheet documents. 

With GroupDocs.Redaction API you can remove pages by specifying the page range by means of its relative position (the beginning or the end), zero-based index and the count of pages to remove. At this time the supported formats are: PDF, presentations (Microsoft PowerPoint, OpenOffice Presentations), word processing documents (Microsoft Word, OpenOffice Texts, Rich Text Files), spreadsheets (Microsoft Excel, OpenOffice Spreadsheets, etc.) and multi-frame images.

## Remove page range

In the example below, we remove 2nd, 3rd and 4th pages from the document, if the document has enough pages:

**C#**

```csharp
using (Redactor redactor = new Redactor("sample.pdf"))
{
    // Removes 3 pages starting from 2nd one, requires at least 4 pages
    if (redactor.GetDocumentInfo().PageCount >= 4)
    {
        redactor.Apply(new RemovePageRedaction(PageSeekOrigin.Begin, 1, 3));
        redactor.Save();
    }
}
```

## Remove last page

In some cases you might need to delete the last page or a number of pages, no matter how many pages are there.

The following example demonstrates how to remove the last page from a document:

**C#**

```csharp
using (Redactor redactor = new Redactor("sample.pdf"))
{
    // Requires at least 1 page
    if (redactor.GetDocumentInfo().PageCount >= 1)
    {
        redactor.Apply(new RemovePageRedaction(PageSeekOrigin.End, 0, 1));
        redactor.Save();
    }
}
```

## Remove frame from image

In case of a multi-frame image you might need to delete a number of frames (treated as "pages").

The following example demonstrates how to remove 3 frames from an animated GIF image:

**C#**

```csharp
using (Redactor redactor = new Redactor("sample.gif"))
{
    // Removes 5 frames starting from 3nd one, requires at least 7 frames
    if (redactor.GetDocumentInfo().PageCount >= 7)
    {
        redactor.Apply(new RemovePageRedaction(PageSeekOrigin.Begin, 2, 5));
        redactor.Save();
    }
}
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
