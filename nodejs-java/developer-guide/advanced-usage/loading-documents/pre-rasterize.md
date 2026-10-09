---
id: pre-rasterize
url: redaction/nodejs-java/pre-rasterize
title: Pre-rasterize
weight: 5
description: "This article shows how to pre-rasterize a document using the redaction API."
keywords: redaction API
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
In some cases, you might need to pre-rasterize the document before opening it and applying redactions. 

For instance, you might need to use an [ImageAreaRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/imagearearedaction/) for a whole page of a document with searchable text and images. In order to do that, you will need to pass the Boolean flag to the [LoadOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/loadoptions/) class constructor.

The following example demonstrates how to pre-rasterize a Microsoft Word document:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');
const Dimension = java.import('java.awt.Dimension');
const Point = java.import('java.awt.Point');

const loadOptions = new redaction.LoadOptions(/*preRasterize*/ true);
const redactor = new redaction.Redactor('sample.docx', loadOptions);
        try 
        {
            // Make changes to the file as a rasterized PDF, e.g. uisng ImageAreaRedaction:
const samplePoint = new Point(516, 311);
const sampleSize = new Dimension(170, 35);
const result = redactor.apply(new redaction.ImageAreaRedaction(samplePoint,
                new redaction.RegionReplacementOptions(Color.RED, sampleSize)));
            if (result.getStatus() !== redaction.RedactionStatus.Failed)
            {
                    redactor.save();
            };
        }
        finally {
  redactor.close();
}
}
```

