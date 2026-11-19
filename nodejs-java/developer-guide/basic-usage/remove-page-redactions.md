---
id: remove-page-redactions
url: redaction/nodejs-java/remove-page-redactions
title: Remove page redactions
weight: 10
description: This article shows that how to remove pages with sensitive data from your PDF, presentation and spreadsheet documents.
keywords: remove page,PDF,Excel,PowerPoint,spreadsheet,presentation
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

GroupDocs.Redaction allows to easily to remove pages from PDF documents, slides from presentations and worksheets from spreadsheet documents. 

With GroupDocs.Redaction API you can remove pages by specifying the page range by means of its relative position (the beginning or the end), zero-based index and the count of pages to remove. At this time the supported formats are: PDF, presentations (Microsoft PowerPoint, OpenOffice Presentations), word processing documents (Microsoft Word, OpenOffice Texts, Rich Text Files), spreadsheets (Microsoft Excel, OpenOffice Spreadsheets, etc.) and multi-frame images.

## Remove page range

In the example below, we remove 2nd, 3rd and 4th pages from the document, if the document has enough pages:

{{< tabs "code-example-remove-page-range" >}}
{{< tab "remove_page_range.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.pdf');
try 
{
const info = redactor.getDocumentInfo();
const startIndex = 1, pagesToDelete = 1;
    // Removes 1 page starting from 2nd one, requires at least 2 pages
    if (info.getPageCount() >= 2)
    {
        redactor.apply(new redaction.RemovePageRedaction(redaction.PageSeekOrigin.Begin, startIndex, pagesToDelete));
const tmp0 = new redaction.SaveOptions();
        tmp0.setAddSuffix(true);
        tmp0.setRasterizeToPDF(false);
        redactor.save(tmp0);
    }
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/basic-usage/remove-page-redactions/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multipage_sample_redacted.pdf" >}}  
```text
Binary file (PDF, 190 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/basic-usage/remove-page-redactions/CodeExampleRemovePageRange/multipage_sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

## Remove last page

In some cases you might need to delete the last page or a number of pages, no matter how many pages are there.

The following example demonstrates how to remove the last page from a document:

{{< tabs "code-example-remove-last-page" >}}
{{< tab "remove_last_page.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.pdf');
try 
{
    // Requires at least 1 page
    if (redactor.getDocumentInfo().getPageCount() >= 1)
    {
        redactor.apply(new redaction.RemovePageRedaction(redaction.PageSeekOrigin.End, 0, 1));
const tmp0 = new redaction.SaveOptions();
        tmp0.setAddSuffix(true);
        tmp0.setRasterizeToPDF(false);
        redactor.save(tmp0);
    }
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/basic-usage/remove-page-redactions/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multipage_sample_redacted.pdf" >}}  
```text
Binary file (PDF, 190 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/basic-usage/remove-page-redactions/CodeExampleRemoveLastPage/multipage_sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

## Remove frame from image

In case of a multi-frame image you might need to delete a number of frames (treated as "pages").

The following example demonstrates how to remove 3 frames from an animated GIF image:

{{< tabs "code-example-remove-frame-from-image" >}}
{{< tab "remove_frame_from_image.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Animated.gif');
try 
{
    // Removes 5 frames starting from 3nd one, requires at least 7 frames
    if (redactor.getDocumentInfo().getPageCount() >= 7)
    {
        redactor.apply(new redaction.RemovePageRedaction(redaction.PageSeekOrigin.Begin, 2, 5));
        redactor.save();
    }
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.gif" >}}
{{< tab-text >}}
`sample.gif` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/basic-usage/remove-page-redactions/sample.gif) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.gif" >}}  
```text
Binary file (GIF, 704 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/basic-usage/remove-page-redactions/CodeExampleRemoveFrameFromImage/sample_redacted.gif)
{{< /tab >}}
{{< /tabs >}}
    
    

