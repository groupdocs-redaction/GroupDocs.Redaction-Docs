---
id: features-overview
url: redaction/python-net/features-overview
title: Features Overview
linkTitle: Features Overview
weight: 1
description: "GroupDocs.Redaction for Python via .NET removes sensitive information from documents through a single, format-independent API — text, metadata, image areas, annotations, and whole pages — and saves the result in the original format or as a sanitized PDF."
keywords: redact pdf, redact word, metadata redaction, image redaction, annotation redaction, remove page, rasterize pdf, redaction policy, python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Redaction for Python via .NET removes or permanently obscures sensitive information across a wide range of [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}). Every redaction follows the same workflow: open a document with `Redactor`, apply one or more redactions with `apply()`, then `save()` the cleaned result either in its original format or as a sanitized PDF. The capabilities below can be combined freely in a single pass.

## Text redaction

Find and replace text by an exact phrase or by a regular expression, covering both whole words and complex patterns such as e-mail addresses, phone numbers, or national ID numbers. Matched text can be replaced with substitute text or covered by a colored box so the original content cannot be recovered. In spreadsheets you can narrow the search to a single worksheet or column. See [Text Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/text-redactions.md" >}}).

## Metadata redaction

Erase or rewrite document metadata — author, title, company, comments, and EXIF data on images — so no sensitive details leak through document properties. You can clear all metadata, target specific fields, or replace values with new ones. See [Metadata Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/metadata-redactions.md" >}}).

## Image-area redaction

Black out a rectangular region of an embedded image or a scanned page by drawing a filled box over a given area — useful for hiding signatures, photos, headers, or footers where confidential data is expected to appear. See [Image Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/image-redactions.md" >}}).

## Annotation redaction

Rewrite or delete annotations, comments, and notes. You can remove every annotation or use a regular expression to match only the ones that contain sensitive text. See [Annotation Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/annotation-redactions.md" >}}).

## Page removal

Remove whole pages from PDF documents, slides from presentations, and worksheets from spreadsheets. You specify a starting page and a count, together with the direction relative to the starting point. See [Remove Page Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/remove-page-redactions.md" >}}).

## Rasterization to PDF

Save the cleaned document as a PDF whose pages are rendered as raster images. The resulting file contains no searchable text and none of the original metadata, so the removed content cannot be recovered. Rasterization is the right choice when you must hand a document to third parties or conform to regulations that require PDF. You can select specific pages and request PDF/A compliance through the advanced rasterization options. See [Save in Rasterized PDF]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf.md" >}}) and [Advanced Rasterization Options]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options.md" >}}).

## Redaction policies

Group several redactions into a reusable policy and apply the same set of rules consistently across many documents — ideal for recurring tasks such as scrubbing a standard set of fields before publishing. See [Use Redaction Policies]({{< ref "redaction/python-net/developer-guide/advanced-usage/use-redaction-policies.md" >}}).

## Loading and saving

Load documents from a local path or from a stream, including password-protected files, and optionally pre-rasterize a document before redacting. When saving, keep the original format for further editing, overwrite the original file, rasterize to PDF, or write to a stream. See [Loading Documents]({{< ref "redaction/python-net/developer-guide/advanced-usage/loading-documents/_index.md" >}}) and [Saving Documents]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/_index.md" >}}).

## On-premise

GroupDocs.Redaction for Python via .NET runs entirely on your own infrastructure — your documents never leave your environment. The package is a self-contained wheel that bundles everything it needs, so no Microsoft Office, OpenOffice, Adobe Acrobat, or separate runtime has to be installed. See [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) for the supported platforms and native dependencies.
