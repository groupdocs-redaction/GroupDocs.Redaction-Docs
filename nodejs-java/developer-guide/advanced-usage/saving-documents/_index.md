---
id: saving-documents
url: redaction/nodejs-java/saving-documents
title: Saving documents
weight: 2
description: "Save redacted documents in original format or as rasterized PDF."
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
---
By default `save()` rasterizes pages to a single PDF and may add a suffix. Use `SaveOptions` to keep the original format (`setRasterizeToPDF(false)`), control suffixes, or set Word OOXML compliance via `getWordprocessingSaveOptions()`.
