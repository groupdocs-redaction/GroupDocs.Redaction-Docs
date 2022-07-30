---
id: get-document-page-preview
url: redaction/java/get-document-page-preview
title: Get document page preview
weight: 3
description: This article shows the implementation of Redactor class which supports the rendering of the document preview in JPEG, PNG and BMP.
keywords: redactor, jpeg, png, bmp
productName: GroupDocs.Redaction for Java
hideChildren: False
---

In GroupDocs.Redaction, *Redactor* class supports rendering of the document preview in on of these image formats:

*   JPEG Image
*   Portable Network Graphics
*   Bitmap Image File

The following example demonstrates how to get a single page preview of the document.

```java
// Test file
final String testFile = "D:\\sample.pdf";
// Take preview of the first page
int testPageNumber = 1;
// Preview file name
final String previewFileName = String.format("%s_page%d.png", testFile, testPageNumber);
// Load the document to generate preview
final Redactor redactor = new Redactor(testFile);
try 
{
    PreviewOptions options = new PreviewOptions(new ICreatePageStream() { 
        @Override
        public java.io.OutputStream createPageStream(int pageNumber) { 
            try {
                return new java.io.FileOutputStream(previewFileName); 
            } catch (java.io.FileNotFoundException ex) {
                System.out.printf("Failed to create preview file %s: \"%s\"\n\n", previewFileName, ex.toString());
                return null;
            }
        } 
    });
    options.setHeight(640);
    options.setWidth(480);
    options.setPageNumbers(new int[] { testPageNumber });
    options.setPreviewFormat(PreviewFormats.Png);
    redactor.generatePreview(options);            
    System.out.printf("\nPreview for page %d  was saved to \"%s\"\n\n", testPageNumber, previewFileName);
}
finally { redactor.close(); }
```
