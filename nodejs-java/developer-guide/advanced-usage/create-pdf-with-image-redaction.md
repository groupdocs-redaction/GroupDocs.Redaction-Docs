---
id: create-pdf-with-image-redaction
url: redaction/nodejs-java/create-pdf-with-image-redaction
title: Create PDF with Image Redaction
weight: 7
description: This article shows how to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text.
keywords: redact
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

In some cases you might need to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text. With GroupDocs.Redaction you can use the following approach:  

*   open the document and apply all required redactions to the document's body (text, annotations, etc.);
    
*   save it as a rasterized PDF file (containing images of the original document's pages);
    
*   apply ImageAreaRedaction to remove specific areas on the pages within the PDF document.  
    
The following example demonstrates how to create a rasterized PDF from a Microsoft Word document and apply image redactions to its pages:


```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const inputStream = null;
// Rasterize the document before applying redactions
const raterizer = new redaction.Redactor('C:\\Temp\\sample.docx');
try 
{
    // Perform annotation and textual redactions, if needed
const stream = new ByteArrayOutputStream();
const options = new redaction.RasterizationOptions();
    options.setEnabled(true);
    raterizer.save(stream, options);
    inputStream = new ByteArrayInputStream(stream.toByteArray());  
    stream.close();
}
finally {
  raterizer.close();
}
if (inputStream !== null)
{
    // Re-open the rasterized PDF document to redact its pages as images
const redactor = new redaction.Redactor(inputStream);
    try 
    {
const result = redactor.apply(new redaction.ImageAreaRedaction(new Point(1160, 2375),
            new redaction.RegionReplacementOptions(Color.BLUE, new Dimension(1050, 720))));
        if (result.getStatus() !== redaction.RedactionStatus.Failed)
        {
const fileStream = new FileOutputStream('C:\\Temp\\sample_docx_Raster.pdf');
            try 
            {
const options = new redaction.RasterizationOptions();
                options.setEnabled(false);
                redactor.save(fileStream, options);
            }
            finally {
  fileStream.close();
}
        }         
    }
    finally { redactor.close(); inputStream.close(); }
}
```

Please, note that you don't have to use GroupDocs.Redaction to create a rasterized PDF from an office document. You will be able to use it, if you don't have any other tool for that.

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Node.js via Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document parser App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
