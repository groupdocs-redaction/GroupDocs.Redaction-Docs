---
id: supported-document-formats
url: redaction/python-net/supported-document-formats
title: Supported Document Formats
second_title: Documentation
weight: 4
description: "GroupDocs.Redaction for Python via .NET redacts 40+ formats: PDF, Word, Excel, PowerPoint and OpenDocument files, images (JPEG, PNG, TIFF, WEBP, DjVu), HTML, Markdown, CSV and text, with what each redaction does on each format."
keywords: file formats, supported formats, Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenDocument, PDF, DOCX, DOC, RTF, ODT, XLSX, XLS, XLSB, ODS, CSV, PPTX, PPT, ODP, JPEG, PNG, TIFF, WEBP, DJVU, HTML, Markdown
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: false
---

## Supported File Formats

GroupDocs.Redaction for Python via .NET opens, redacts and saves 40+ document and image formats. Every format below saves in its own format and as a rasterized PDF, the default of `save()`.

The table shows what each kind of redaction does on each format. It was measured on GroupDocs.Redaction for Python via .NET 26.11, on Windows and Linux, with one document per format: **✓** the redaction applies, **–** the engine skips it for that format (the format has no such content), **✗** the redaction fails, or reports `APPLIED` and leaves the content in place.

- **Text**: `ExactPhraseRedaction` and `RegexRedaction` with a replacement text. **OCR**: text in an image is found through an OCR connector; see [Using OCR]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-ocr/_index.md" >}}).
- **Box over text**: the same redactions with `ReplacementOptions(Color...)`, which draw a box instead of replacing the text.
- **Metadata**: `EraseMetadataRedaction` and `MetadataSearchRedaction`. **Comments**: `AnnotationRedaction` and `DeleteAnnotationRedaction`.
- **Image areas**: `ImageAreaRedaction`, in images and in the images a document embeds. **Remove pages**: `RemovePageRedaction`.

| Format | Description | Text | Box over text | Metadata | Comments | Image areas | Remove pages |
| --- | --- | :---: | :---: | :---: | :---: | :---: | :---: |
| [PDF](https://docs.fileformat.com/pdf/) | Portable Document Format | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOC](https://docs.fileformat.com/word-processing/doc/) | Microsoft Word 97-2003 Document | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOCX](https://docs.fileformat.com/word-processing/docx/) | Office Open XML WordprocessingML Document | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOCM](https://docs.fileformat.com/word-processing/docm/) | Office Open XML WordprocessingML Macro-Enabled Document | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOT](https://docs.fileformat.com/word-processing/dot/) | Microsoft Word 97-2003 Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOTX](https://docs.fileformat.com/word-processing/dotx/) | Office Open XML WordprocessingML Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [DOTM](https://docs.fileformat.com/word-processing/dotm/) | Office Open XML WordprocessingML Macro-Enabled Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [RTF](https://docs.fileformat.com/word-processing/rtf/) | Rich Text Format | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [ODT](https://docs.fileformat.com/word-processing/odt/) | OpenDocument Text | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [OTT](https://docs.fileformat.com/word-processing/ott/) | OpenDocument Text Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [TXT](https://docs.fileformat.com/word-processing/txt/) | Plain Text | ✓ | – | – | – | – | – |
| [MD](https://docs.fileformat.com/word-processing/md/) | Markdown | ✓ | ✗ | – | – | – | – |
| [XLS](https://docs.fileformat.com/spreadsheet/xls/) | Microsoft Excel 97-2003 Workbook | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLSX](https://docs.fileformat.com/spreadsheet/xlsx/) | Office Open XML Workbook | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLSM](https://docs.fileformat.com/spreadsheet/xlsm/) | Office Open XML Macro-Enabled Workbook | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLSB](https://docs.fileformat.com/spreadsheet/xlsb/) | Excel Binary Workbook | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLT](https://docs.fileformat.com/spreadsheet/xlt/) | Microsoft Excel 97-2003 Template | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLTX](https://docs.fileformat.com/spreadsheet/xltx/) | Office Open XML Workbook Template | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [XLTM](https://docs.fileformat.com/spreadsheet/xltm/) | Office Open XML Macro-Enabled Workbook Template | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [ODS](https://docs.fileformat.com/spreadsheet/ods/) | OpenDocument Spreadsheet | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [OTS](https://docs.fileformat.com/spreadsheet/ots/) | OpenDocument Spreadsheet Template | ✓ | ✓ | ✓ | ✓ | – | ✓ |
| [CSV](https://docs.fileformat.com/spreadsheet/csv/) | Comma-Separated Values | ✓ | – | ✓ | ✓ | – | ✓ |
| [TAB](https://docs.fileformat.com/spreadsheet/tsv/) | Tab-Separated Values | ✓ | – | ✓ | ✓ | – | ✓ |
| [PPT](https://docs.fileformat.com/presentation/ppt/) | Microsoft PowerPoint 97-2003 Presentation | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [PPTX](https://docs.fileformat.com/presentation/pptx/) | Office Open XML Presentation | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [PPTM](https://docs.fileformat.com/presentation/pptm/) | Office Open XML Macro-Enabled Presentation | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [PPS](https://docs.fileformat.com/presentation/pps/) | Microsoft PowerPoint 97-2003 Slide Show | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [PPSX](https://docs.fileformat.com/presentation/ppsx/) | Office Open XML Slide Show | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [PPSM](https://docs.fileformat.com/presentation/ppsm/) | Office Open XML Macro-Enabled Slide Show | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [POTX](https://docs.fileformat.com/presentation/potx/) | Office Open XML Presentation Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [POTM](https://docs.fileformat.com/presentation/potm/) | Office Open XML Macro-Enabled Presentation Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [ODP](https://docs.fileformat.com/presentation/odp/) | OpenDocument Presentation | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [OTP](https://docs.fileformat.com/presentation/otp/) | OpenDocument Presentation Template | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [BMP](https://docs.fileformat.com/image/bmp/) | Bitmap Image | OCR | – | – | – | ✓ | – |
| [GIF](https://docs.fileformat.com/image/gif/) | Graphics Interchange Format | OCR | – | ✗ | – | ✓ | ✗ |
| [JPEG](https://docs.fileformat.com/image/jpeg/) | JPEG Image | OCR | – | ✓ | – | ✓ | – |
| [PNG](https://docs.fileformat.com/image/png/) | Portable Network Graphics | OCR | – | ✗ | – | ✓ | – |
| [TIFF](https://docs.fileformat.com/image/tiff/) | Tagged Image File Format | OCR | – | ✗ | – | ✓ | ✓ |
| [WEBP](https://docs.fileformat.com/image/webp/) | WebP Image | OCR | – | ✗ | – | ✓ | ✓ |
| [DJVU](https://docs.fileformat.com/image/djvu/) | DjVu Document | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| [HTML](https://docs.fileformat.com/web/html/) | HyperText Markup Language | ✓ | ✗ | – | – | – | – |

In HTML and Markdown a box cannot be drawn: use a replacement text. Plain text, CSV and TAB files have no room for a box either, and the engine skips it.

Removing pages of a multi-frame image, measured on 8 frames:

- **TIFF:** loses the pages asked for; removing the only page of a single-page TIFF reports `FAILED`.
- **Animated WEBP:** loses the last frame or a range as asked, but removing the first frame raises "Index was out of range".
- **Animated GIF:** loses fewer frames than asked, although the redaction reports `APPLIED`. Removing the first or the last of 8 frames leaves 8, and removing 5 from the third leaves 5.

Metadata was checked in the saved files for Office Open XML, OpenDocument, RTF, PDF and image files:

- **Office Open XML, OpenDocument and RTF** files lose the properties the filter names.
- **A PDF saved as PDF** keeps the properties that only its document information dictionary holds. The engine finds a PDF's properties through its XMP packet, so a PDF whose author is written only in the dictionary keeps it, and the redaction still reports `APPLIED`. A rasterized PDF, the default of `save()`, carries none of the original's author, title or subject.
- **Images:** JPEG files have their EXIF values blanked. PNG files lose their text chunks and keep their EXIF data. WEBP, TIFF and GIF files keep their metadata, although the redaction reports `APPLIED`. BMP files have no metadata.

{{< alert style="tip" >}}

**Can’t find your file format?**

We’re here to help! Please post a request on our [Free Support Forum](https://forum.groupdocs.com/c/redaction/33), and our team will assist you.

{{< /alert >}}
