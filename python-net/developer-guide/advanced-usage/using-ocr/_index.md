---
id: using-ocr
url: redaction/python-net/using-ocr
title: Using OCR to redact image documents
linkTitle: Using OCR
weight: 4
description: "Redact text in scanned documents and embedded images with GroupDocs.Redaction for Python via .NET by plugging in an OCR engine of your choice."
keywords: OCR, scanned document, image, IOcrConnector, ocr_connector, Tesseract, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
GroupDocs.Redaction redacts text it can only see in pictures, given an OCR engine:

* image files, such as scans of printed documents (PNG, JPG and others);
* images embedded in documents (PDF, DOCX and others).

GroupDocs.Redaction does not ship an OCR engine. You plug one in through an OCR connector, the Python side of the [IOcrConnector](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.integration.ocr/iocrconnector/) interface, and pass it to [RedactorSettings](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/redactorsettings/). Any engine works, local or a web service, as long as it reports each recognized word with its position.

## In this section

- [OCR usage basics]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-ocr/ocr-usage-basics.md" >}}) — what a connector receives and returns, with a connector you can run without an OCR engine.
- [Use Tesseract OCR]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-ocr/use-tesseract-ocr.md" >}}) — a connector built on the open-source Tesseract engine and `pytesseract`.
