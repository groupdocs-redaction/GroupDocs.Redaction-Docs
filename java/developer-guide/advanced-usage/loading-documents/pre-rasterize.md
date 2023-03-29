---
id: pre-rasterize
url: redaction/java/pre-rasterize
title: Pre-rasterize
weight: 5
description: "This article shows how to pre-rasterize a document using the redaction API."
keywords: redaction API
productName: GroupDocs.Redaction for Java
hideChildren: False
---
In some cases, you might need to pre-rasterize the document before opening it and applying redactions. 

For instance, you might need to use an [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/imagearearedaction/) for a whole page of a document with searchable text and images. In order to do that, you will need to pass the Boolean flag to the [LoadOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/loadoptions/) class constructor.

The following example demonstrates how to pre-rasterize a Microsoft Word document:

```java
        LoadOptions loadOptions = new LoadOptions(/*preRasterize*/ true);
        final Redactor redactor = new Redactor("sample.docx", loadOptions);
        try 
        {
            // Make changes to the file as a rasterized PDF, e.g. uisng ImageAreaRedaction:
            java.awt.Point samplePoint = new java.awt.Point(516, 311);
            java.awt.Dimension sampleSize = new java.awt.Dimension(170, 35);
            RedactorChangeLog result = redactor.apply(new ImageAreaRedaction(samplePoint,
                new RegionReplacementOptions(java.awt.Color.RED, sampleSize)));
            if (result.getStatus() != RedactionStatus.Failed)
            {
                    redactor.save();
            };
        }
        finally { redactor.close(); }
}
```

