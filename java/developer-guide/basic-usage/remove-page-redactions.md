---
id: remove-page-redactions
url: redaction/java/remove-page-redactions
title: Remove page redactions
weight: 10
description: This article shows that how to remove pages with sensitive data from your PDF, presentation and spreadsheet documents.
keywords: remove page,PDF,Excel,PowerPoint,spreadsheet,presentation
productName: GroupDocs.Redaction for Java
hideChildren: False
---

GroupDocs.Redaction allows to easily to remove pages from PDF documents, slides from presentations and worksheets from spreadsheet documents. 

With GroupDocs.Redaction API you can remove pages by specifying the page range by means of its relative position (the beginning or the end), zero-based index and the count of pages to remove. At this time the supported formats are: PDF, presentations (Microsoft PowerPoint, OpenOffice Presentations), word processing documents (Microsoft Word, OpenOffice Texts, Rich Text Files), spreadsheets (Microsoft Excel, OpenOffice Spreadsheets, etc.) and multi-frame images.

## Remove page range

In the example below, we remove 2nd, 3rd and 4th pages from the document, if the document has enough pages:

```java
final Redactor redactor  = new Redactor("Sample.pdf");
try 
{
    IDocumentInfo info = redactor.getDocumentInfo();
    int startIndex = 1, pagesToDelete = 1;
    // Removes 1 page starting from 2nd one, requires at least 2 pages
    if (info.getPageCount() >= 2)
    {
        redactor.apply(new RemovePageRedaction(PageSeekOrigin.Begin, startIndex, pagesToDelete));
        SaveOptions tmp0 = new  SaveOptions();
        tmp0.setAddSuffix(true);
        tmp0.setRasterizeToPDF(false);
        redactor.save(tmp0);
    }
}
finally { redactor.close(); }
```

## Remove last page

In some cases you might need to delete the last page or a number of pages, no matter how many pages are there.

The following example demonstrates how to remove the last page from a document:

```java
final Redactor redactor  = new Redactor("Sample.pdf");
try 
{
    // Requires at least 1 page
    if (redactor.getDocumentInfo().getPageCount() >= 1)
    {
        redactor.apply(new RemovePageRedaction(PageSeekOrigin.End, 0, 1));
        SaveOptions tmp0 = new  SaveOptions();
        tmp0.setAddSuffix(true);
        tmp0.setRasterizeToPDF(false);
        redactor.save(tmp0);
    }
}
finally { redactor.close(); }
```

## Remove frame from image

In case of a multi-frame image you might need to delete a number of frames (treated as "pages").

The following example demonstrates how to remove 3 frames from an animated GIF image:

```java
final Redactor redactor = new Redactor("Animated.gif");
try 
{
    // Removes 5 frames starting from 3nd one, requires at least 7 frames
    if (redactor.getDocumentInfo().getPageCount() >= 7)
    {
        redactor.apply(new RemovePageRedaction(PageSeekOrigin.Begin, 2, 5));
        redactor.save();
    }
}
finally { redactor.close(); }
```
    
    

