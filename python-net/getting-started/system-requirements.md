---
id: system-requirements
url: redaction/python-net/system-requirements
title: System Requirements
linkTitle: System Requirements
weight: 6
description: "GroupDocs.Redaction for Python via .NET ships as a self-contained wheel and runs on Windows, Linux, and macOS without Microsoft Office, OpenOffice, or any other third-party software installed."
keywords: System Requirements, supported operating systems, supported python versions, groupdocs redaction python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

{{< alert style="info" >}}
GroupDocs.Redaction for Python via .NET operates independently of external software like Microsoft Word, Excel, PowerPoint, or Adobe Acrobat. To install it, simply follow one of the methods described in the [Installation]({{< ref "redaction/python-net/getting-started/installation.md" >}}) section.
{{< /alert >}}

## Overview

GroupDocs.Redaction for Python via .NET does not require Microsoft Office, OpenOffice, Adobe Acrobat, or any other external software to be installed. The package is a self-contained wheel that bundles everything it needs, so the only prerequisites are a supported version of Python and the operating-system packages listed below.

## Supported Python Versions

GroupDocs.Redaction for Python via .NET supports the following Python versions:

* Python 3.5
* Python 3.6
* Python 3.7
* Python 3.8
* Python 3.9
* Python 3.10
* Python 3.11
* Python 3.12
* Python 3.13
* Python 3.14

## Supported Operating Systems

The package is distributed as a self-contained wheel that runs on the following platforms:

### Windows

* Windows x64

No additional dependencies are required on Windows.

### Linux

* Linux x64

On Linux you need to install a few system packages for graphics, fonts, and globalization:

```bash
apt install libgdiplus libfontconfig1 libicu-dev ttf-mscorefonts-installer
```

### macOS

* macOS x64 (Intel)
* macOS ARM64 (Apple Silicon)

On macOS install the graphics library via Homebrew:

```bash
brew install mono-libgdiplus
```

## Platform-Specific Feature Support

{{< alert style="warning" >}}
**Rasterization to PDF and image-area redaction currently require Windows.** In version 26.6.0 the bundled engine renders rasterized output and processes images through `System.Drawing.Common`, which the embedded .NET runtime supports only on Windows. On Linux and macOS these specific operations raise a `System.PlatformNotSupportedException` ("System.Drawing.Common is not supported on this platform"). Installing `libgdiplus` / `mono-libgdiplus` does **not** lift this restriction.
{{< /alert >}}

The following redaction operations work on **all** platforms — Windows, Linux, and macOS:

* Text redaction (exact phrase and regular expression)
* Metadata redaction (erase, and search-and-replace)
* Annotation redaction (rewrite and delete)
* Page removal
* Saving in the **original** format with `SaveOptions(rasterize_to_pdf=False)`

The following operations currently require **Windows**:

* The default `save()` — which rasterizes the result to a PDF — and any `RasterizationOptions` or rasterized-PDF save path
* `ImageAreaRedaction` and image cleaning / image-export operations

On Linux and macOS, keep the source format with `SaveOptions(rasterize_to_pdf=False)`, or perform the rasterization and image-redaction steps on Windows.

## No Third-Party Software Required

Unlike many document-processing tools, GroupDocs.Redaction for Python via .NET does not depend on Microsoft Office, OpenOffice, Adobe Acrobat, or any other application being installed on the machine. All loading, redacting, and saving of Word Processing documents, Spreadsheets, Presentations, PDFs, and images is performed entirely by the bundled engine.
