---
id: saving-documents
url: redaction/python-net/saving-documents
title: Saving documents
linkTitle: Saving documents
weight: 2
description: "Save redacted documents with GroupDocs.Redaction for Python via .NET — keep the original format, rasterize to PDF, save to a stream, overwrite the source, select pages, and apply advanced rasterization options."
keywords: save document, rasterize to PDF, save to stream, overwrite original, rasterization options, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

By default `save()` rasterizes every page of the redacted document into images and writes a single PDF next to the source file, so the result can be shared without any chance of recovering the removed content. You control this through the `rasterize_to_pdf` property of `SaveOptions` (or `enabled` on `RasterizationOptions`), and you can redirect the output to a stream for any custom location. The topics below show each saving scenario.

## In this section

- [Save in Original Format]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) — keep the source format instead of rasterizing to PDF.
- [Save in Rasterized PDF]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf.md" >}}) — flatten the result to a rasterized PDF so redactions are irreversible.
- [Save Overwriting Original File]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-overwriting-original-file.md" >}}) — write the redacted output back over the source document.
- [Save to Stream]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-to-stream.md" >}}) — write the result to any writable stream.
- [Save with Default Options]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-with-default-options.md" >}}) — use the default save behavior.
- [Select Specific Pages for Rasterized PDF]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/select-specific-pages-for-rasterized-pdf.md" >}}) — rasterize only a chosen page range.
- [Use Advanced Rasterization Options]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options.md" >}}) — add anti-extraction effects (noise, tilt, border, grayscale) and set PDF/A compliance.
