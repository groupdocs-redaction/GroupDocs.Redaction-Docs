---
id: create-pdf-with-image-redaction
url: redaction/java/create-pdf-with-image-redaction
title: Create PDF with Image Redaction
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---

In some cases you might need to redact the pages of a document as images, redacting entire areas of the page instead or in addition to a specific text. With GroupDocs.Redaction you can use the following approach:  

*   open the document and apply all required redactions to the document's body (text, annotations, etc.);
    
*   save it as a rasterized PDF file (containing images of the original document's pages);
    
*   apply ImageAreaRedaction to remove specific areas on the pages within the PDF document.  
    
The following example demonstrates how to create a rasterized PDF from a Microsoft Word document and apply image redactions to its pages:


```java
ByteArrayInputStream inputStream = null;
// Rasterize the document before applying redactions
final Redactor raterizer = new Redactor("C:\\Temp\\sample.docx");
try 
{
    // Perform annotation and textual redactions, if needed
    ByteArrayOutputStream stream = new ByteArrayOutputStream();
    RasterizationOptions options = new RasterizationOptions();
    options.setEnabled(true);
    raterizer.save(stream, options);
    inputStream = new ByteArrayInputStream(stream.toByteArray());  
    stream.close();
}
finally { raterizer.close(); }
if (inputStream != null)
{
    // Re-open the rasterized PDF document to redact its pages as images
    final Redactor redactor = new Redactor(inputStream);
    try 
    {
        RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(new java.awt.Point(1160, 2375),
            new RegionReplacementOptions(java.awt.Color.BLUE, new java.awt.Dimension(1050, 720))));
        if (result.getStatus() != RedactionStatus.Failed)
        {
            final FileOutputStream fileStream = new FileOutputStream("C:\\Temp\\sample_docx_Raster.pdf");
            try 
            {
                RasterizationOptions options = new  RasterizationOptions();
                options.setEnabled(false);
                redactor.save(fileStream, options);
            }
            finally { fileStream.close(); }
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
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document parser App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
