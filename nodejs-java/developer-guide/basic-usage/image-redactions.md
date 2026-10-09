---
id: image-redactions
url: redaction/nodejs-java/image-redactions
title: Image redactions
weight: 8
description: "Cover a rectangular area of an image with a solid color."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const Color = java.import('java.awt.Color');
const Point = java.import('java.awt.Point');
const Dimension = java.import('java.awt.Dimension');

const redactor = new redaction.Redactor('sample.jpg');
try {
  const options = new redaction.RegionReplacementOptions(
    Color.BLUE,
    new Dimension(170, 35));
  redactor.apply(new redaction.ImageAreaRedaction(new Point(516, 311), options));
  redactor.save();
} finally {
  redactor.close();
}
```

`Point`, `Dimension`, and `Color` come from `java.awt` through the Java bridge (same types as GroupDocs.Redaction for Java).
