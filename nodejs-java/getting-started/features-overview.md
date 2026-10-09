---
id: features-overview
url: redaction/nodejs-java/features-overview
title: Features overview
weight: 1
description: "Main redaction capabilities available in GroupDocs.Redaction for Node.js via Java."
keywords: features, text redaction, metadata, rasterization
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
GroupDocs.Redaction provides a format-independent API to sanitize documents before sharing or publishing.

## Document redaction

You can redact PDF, Word, Excel, PowerPoint, images, and related formats: replace or hide text, scrub metadata, clean annotations, black out image regions, and remove pages. After redaction, save in the original format for further editing, or rasterize to PDF so redacted content is no longer searchable.

### Rasterization

Rasterization creates a PDF of page images. The result has no searchable text from the original body and no original metadata. Use it when you must share a locked-down PDF across platforms.

### Keeping original format

Saving without rasterization keeps the document editable in its native application after sensitive data is removed. For Word OOXML files you can also set compliance via `SaveOptions` (see [Save Word with OOXML compliance]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/saving-documents/save-word-with-ooxml-compliance.md" >}})).
