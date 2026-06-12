---
id: how-to-run-examples
url: redaction/python-net/how-to-run-examples
title: How to Run Examples
linkTitle: How to Run Examples
weight: 7
description: "Clone the ready-to-run GroupDocs.Redaction for Python via .NET examples repository, set up a virtual environment, and run every documented scenario locally or in Docker."
keywords: groupdocs redaction python, examples, run examples, docker, ci, python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

{{< alert style="warning" >}}Before running an example make sure that GroupDocs.Redaction for Python via .NET has been installed successfully.{{< /alert >}}

The complete examples project for **GroupDocs.Redaction for Python via .NET** is hosted on [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET). It contains standalone, runnable scripts together with the sample documents they use, so the examples work out of the box.

## Prerequisites

- [Python](https://www.python.org/) 3.5 – 3.14 installed and on your `PATH`.
- [git](https://git-scm.com/) to clone the repository (or download the ZIP).
- On Linux and macOS, the native libraries listed in the [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) (`libgdiplus`, `libfontconfig1`, `libicu-dev`, and fonts).
- Optionally, a GroupDocs.Redaction license to remove the [evaluation limitations]({{< ref "redaction/python-net/getting-started/licensing-and-subscription.md" >}}).

## Get the code

Clone the repository with your favourite git client, or download the ZIP from GitHub:

```bash
git clone https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET.git
cd GroupDocs.Redaction-for-Python-via-.NET
```

## Project Structure

The examples live under the `Examples/` folder, organized by topic. Directory names are kebab-case and each script is standalone:

```text
GroupDocs.Redaction-for-Python-via-.NET/
├── Dockerfile
└── Examples/
    ├── requirements.txt
    ├── run_all_examples.py
    ├── licensing/
    │   └── set_license_from_file.py
    ├── getting-started/
    │   └── hello-world/
    │       └── hello_world.py
    └── developer-guide/
        ├── basic-usage/
        │   ├── text-redactions.py
        │   ├── metadata-redactions.py
        │   ├── image-redactions.py
        │   ├── annotation-redactions.py
        │   └── remove-page-redactions.py
        └── advanced-usage/
            ├── use-redaction-policies.py
            ├── loading-documents/
            └── saving-documents/
```

## Setup

Create and activate a virtual environment, then install the dependencies listed in `Examples/requirements.txt`:

{{< tabs "setup-venv">}}
{{< tab "Windows" >}}
```ps
py -m venv .venv
.venv\Scripts\activate
py -m pip install -r Examples/requirements.txt
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r Examples/requirements.txt
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r Examples/requirements.txt
```
{{< /tab >}}
{{< /tabs >}}

To run the examples without evaluation limitations, point the `GROUPDOCS_LIC_PATH` environment variable at your license file. The example scripts read this variable and apply the license automatically:

{{< tabs "setup-license">}}
{{< tab "Windows" >}}
```ps
$env:GROUPDOCS_LIC_PATH = "C:\path\to\GroupDocs.Redaction.lic"
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
export GROUPDOCS_LIC_PATH="/path/to/GroupDocs.Redaction.lic"
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
export GROUPDOCS_LIC_PATH="/path/to/GroupDocs.Redaction.lic"
```
{{< /tab >}}
{{< /tabs >}}

See [Licensing and Evaluation]({{< ref "redaction/python-net/getting-started/licensing-and-subscription.md" >}}) for details on obtaining and applying a license.

## Run

Run every example at once with the runner script:

```bash
python Examples/run_all_examples.py
```

Or run a single example by passing its path directly:

```bash
python Examples/developer-guide/basic-usage/text-redactions.py
```

The repository ships with all the sample documents and resources used by the examples, so the scripts run out of the box.

{{< alert style="info" >}}Without a license the examples run in evaluation mode, which raises a `TrialLimitationsException` if more than one document is opened in the same process. The `run_all_examples.py` runner launches each example in its own process so they all complete even unlicensed, but redaction output is limited (one redaction per document, up to four replacements, and trial badges on each page).{{< /alert >}}

## Run with Docker

The repository includes a `Dockerfile` that installs the native dependencies and Python packages so you can run the examples in a clean, reproducible container. From the repository root:

```bash
docker build -t groupdocs-redaction-examples .
docker run --rm groupdocs-redaction-examples
```

To use a license inside the container, mount it and pass `GROUPDOCS_LIC_PATH`:

```bash
docker run --rm \
  -v /path/to/GroupDocs.Redaction.lic:/app/GroupDocs.Redaction.lic:ro \
  -e GROUPDOCS_LIC_PATH=/app/GroupDocs.Redaction.lic \
  groupdocs-redaction-examples
```

## Continuous integration

Because the examples run headlessly and exit with a non-zero status on failure, they fit naturally into a CI pipeline. Install `Examples/requirements.txt`, supply the license through the `GROUPDOCS_LIC_PATH` environment variable (store the license as a protected secret), make sure the Linux native dependencies are present on the runner, and invoke `python Examples/run_all_examples.py` as a build step. The provided `Dockerfile` is a convenient base image for such jobs.

## Troubleshooting

- **"…rasterization / image-export step is not supported on this platform" on Linux/macOS** — expected on non-Windows in 26.6.0. The rasterized-PDF and image-redaction paths use `System.Drawing.Common`, which the bundled runtime supports only on Windows, so they raise `System.PlatformNotSupportedException`. The `run_all_examples.py` runner catches this and logs the note so the suite still completes; the example's text/metadata/annotation steps still run. To exercise rasterization and image redaction, run on Windows, or save in the original format with `SaveOptions(rasterize_to_pdf=False)`. See [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) for the full platform-support matrix. Installing `libgdiplus` does **not** remove this restriction.
- **Missing or substituted fonts** — install fonts so rasterized output (on Windows) matches the original: `apt install libfontconfig1 ttf-mscorefonts-installer`.
- **ICU / globalization errors on Linux** — install ICU: `apt install libicu-dev`.
- **`TrialLimitationsException`** — you are running unlicensed in evaluation mode, which permits only one document open per process, one redaction, and up to four replacements. Set `GROUPDOCS_LIC_PATH` to a valid license to remove these limits.

## Contribute

If you would like to add or improve an example, we encourage you to contribute to the project. All examples in this repository are open source and can be freely used in your own applications. To contribute, fork the repository, edit the code, and create a pull request. We will review the changes and include them if found helpful.
