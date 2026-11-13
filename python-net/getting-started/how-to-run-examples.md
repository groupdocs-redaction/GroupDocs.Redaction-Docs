---
id: how-to-run-examples
url: redaction/python-net/how-to-run-examples
title: How to Run Examples
linkTitle: How to Run Examples
weight: 7
description: "Clone the ready-to-run GroupDocs.Redaction for Python via .NET examples repository, set it up, and run every documented scenario locally, with a license, or in Docker."
keywords: groupdocs redaction python, examples, run examples, docker, ci, python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

The complete project [GroupDocs.Redaction for Python via .NET](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET) with code examples and sample files is hosted on GitHub. Every example of this documentation is there as a script, next to the documents it redacts.

## Prerequisites

- [Python 3.6-3.14](https://www.python.org/downloads/), 64-bit. The package itself supports Python 3.5-3.14; the examples use f-strings.
- On Linux, ICU, fontconfig and fonts (`libicu-dev libfontconfig1 ttf-mscorefonts-installer`). See [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) for what each one is needed for. Windows and macOS need nothing extra.
- For the Tesseract example only, the [Tesseract](https://github.com/tesseract-ocr/tesseract) OCR engine (`apt install tesseract-ocr` on Debian and Ubuntu, `brew install tesseract` on macOS, the installer on Windows), on your `PATH`. The other OCR example uses a stub and needs nothing.

## Get the code

```bash
git clone https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET.git
cd ./GroupDocs.Redaction-for-Python-via-.NET/Examples
```

## Project structure

```
Examples/
├── run_all_examples.py     # Runs every example, each in its own process, and prints a pass/fail summary
├── requirements.txt
├── product-overview/       # The two examples of the product overview
├── licensing/              # Set a license from a file, a stream, or a metered key
├── getting-started/
│   ├── hello-world/        # Cover a name with a box and save a rasterized PDF
│   └── quick-start-guide/  # A Word, a PDF and an Excel document
└── developer-guide/
    ├── basic-usage/        # Text, metadata, image, annotation, spreadsheet and page redactions; file info; previews
    └── advanced-usage/     # Loading and saving options, filters, policies, the callback, logging, OCR
```

The folders follow this documentation: each page's examples are in the folder of that page, with the documents they read.

## Set up

```bash
pip install -r requirements.txt
```

`requirements.txt` installs `groupdocs-redaction-net`, which brings `groupdocs-shared-net`, and `pytesseract` and `Pillow` for the Tesseract example.

To run the examples with the full feature set, apply a license. The simplest way is the `GROUPDOCS_LIC_PATH` environment variable, which the package applies at the first call into the engine:

{{< tabs "set-license" >}}
{{< tab "Windows" >}}
```batch
set GROUPDOCS_LIC_PATH=C:\path\to\GroupDocs.Redaction.lic
```
{{< /tab >}}
{{< tab "Linux / macOS" >}}
```bash
export GROUPDOCS_LIC_PATH=/path/to/GroupDocs.Redaction.lic
```
{{< /tab >}}
{{< /tabs >}}

Without a license the suite still runs, in evaluation mode: a process opens at most 25 documents, every saved page carries an evaluation notice, and long documents are cut short (see [Licensing and Evaluation]({{< ref "redaction/python-net/getting-started/licensing-and-subscription.md" >}})). `run_all_examples.py` starts each example in a process of its own, so the document limit is never reached. The three examples that read the 7-page PDF stop at the evaluation limit for PDFs of more than 4 pages; the runner reports them as notes, not failures.

## Run the examples

Run the full suite, which prints a pass/fail summary at the end:

```bash
python run_all_examples.py
```

You can also run any single example by navigating to its folder and running the script directly. Each example reads its documents from its own folder, and writes its output next to the script:

```bash
cd getting-started/hello-world
python hello_world.py
```

## Run with Docker

The repository ships a `Dockerfile` that builds a Linux image with Python 3.13, the system packages the examples need on Linux (ICU, fontconfig, the Microsoft core fonts and Tesseract), and the package preinstalled from PyPI.

```bash
# Build the image
docker build -t redaction-examples .

# Run unlicensed (evaluation mode)
docker run --rm redaction-examples

# Run with a license mounted from the host
docker run --rm \
    -v /path/to/license:/lic:ro \
    -e GROUPDOCS_LIC_PATH=/lic/your-license.lic \
    redaction-examples
```

## Continuous integration

The `.github/workflows/` directory contains a workflow that runs the full example suite on every push, on `ubuntu-latest` with Python 3.13 and Tesseract. The same run is reproducible locally via the `Dockerfile` above.

## Troubleshooting

- **"Couldn't find a valid ICU package"**, with the Python process ending abruptly (Linux) - install ICU (`libicu-dev` on Debian and Ubuntu). Do not set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT`.
- **`DllNotFoundException` for a presentation** (Linux) - the presentation engine links fontconfig: `sudo apt install libfontconfig1`.
- **`TesseractNotFoundError`** in the Tesseract example - install Tesseract and put it on your `PATH` (see Prerequisites).
- **An evaluation notice on the saved pages, a document cut short, or "At most 4 elements (for any collection) can be viewed in evaluation mode"** - the evaluation mode. Apply a license (see above); a free 30-day [temporary license](https://purchase.groupdocs.com/temporary-license) is available.
- **`LicenseError` at the first call** - `GROUPDOCS_LIC_PATH` names a file that is missing, expired or for another product. The message gives the engine's reason.
- **An `Aspose/Drawing/` folder appears next to an example** (Linux) - the engine's font cache. It goes there only when `~/.local/share` cannot be created, as in a read-only home; set `XDG_DATA_HOME` to a writable folder.
- **The output differs from the output tab** - the tabs come from a run on Linux with the Microsoft core fonts, and a rasterized PDF draws its text with the fonts installed where it runs.

## Contribute

If you would like to add or improve an example, we encourage you to contribute to the project. All examples in this repository are open source and can be freely used in your own applications. Fork the repository, edit the source code, and open a pull request.
