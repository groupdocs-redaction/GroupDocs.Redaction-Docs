---
id: installation
url: redaction/python-net/installation
title: Install GroupDocs.Redaction for Python via .NET
linkTitle: Installation
weight: 1
keywords: install, installation, pip, pypi, wheel, whl, Windows, Linux, macOS, Apple Silicon, manylinux, requirements.txt, GroupDocs.Redaction, python
description: "Install GroupDocs.Redaction for Python via .NET on Windows, Linux, or macOS — from PyPI or from a pre-downloaded wheel, including Intel and Apple Silicon builds."
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Redaction for Python via .NET is distributed as pre-built wheels on [PyPI](https://pypi.org/project/groupdocs-redaction-net/). PyPI hosts a wheel for each supported platform, and `pip` picks the right one. Each wheel is self-contained: it bundles the .NET runtime and every managed dependency, so no Microsoft Office, OpenOffice, Adobe Acrobat or separate .NET install is required. `pip` also installs `groupdocs-shared-net`, a small package that holds the `groupdocs.pydrawing` and `groupdocs.pycore` modules every GroupDocs product shares.

Before installing, confirm your environment matches the supported platforms and Python versions listed in the [System Requirements]({{< ref "redaction/python-net/getting-started/system-requirements.md" >}}) topic. Installing needs pip 20.3 or later.

## Install Package from PyPI

Open a terminal and run the install command for your platform:

{{< tabs "install-pypi">}}
{{< tab "Windows" >}}
```ps
py -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install groupdocs-redaction-net
```
{{< /tab >}}
{{< /tabs >}}

After running the command you should see output similar to:

```bash
Collecting groupdocs-redaction-net
  Downloading groupdocs_redaction_net-26.11.0-py3-none-win_amd64.whl (154.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 154.5/154.5 MB 9.1 MB/s eta 0:00:00
Collecting groupdocs-shared-net>=26.11.0 (from groupdocs-redaction-net)
  Downloading groupdocs_shared_net-26.11.0-py3-none-any.whl (11 kB)
Installing collected packages: groupdocs-shared-net, groupdocs-redaction-net
Successfully installed groupdocs-redaction-net-26.11.0 groupdocs-shared-net-26.11.0
```

The wheel's file name ends with the platform it is built for: `win_amd64` on 64-bit Windows, `manylinux_2_27_x86_64` on Linux x64 with glibc 2.27 or later, `macosx_12_0_x86_64` on Intel Macs and `macosx_12_0_arm64` on Apple Silicon, both with macOS 12 or later.

## Add the Package to `requirements.txt`

For reproducible environments, pin the package version in your `requirements.txt`:

```txt
groupdocs-redaction-net==26.11.0
```

Then install all dependencies in one step:

```bash
pip install -r requirements.txt
```

## Install from Downloaded Wheels

If your build environment cannot reach PyPI, download the wheel for your platform from the [GroupDocs Releases website](https://releases.groupdocs.com/redaction/python-net/), and `groupdocs_shared_net-26.11.0-py3-none-any.whl` from [PyPI](https://pypi.org/project/groupdocs-shared-net/#files) (or with `pip download groupdocs-shared-net==26.11.0` on a machine that can reach it). Wheels are published for four platforms:

- **Windows 64-bit**: file name ends with `win_amd64.whl`
- **Linux x64 (glibc 2.27+)**: file name ends with `manylinux_2_27_x86_64.whl`
- **macOS Intel (12+)**: file name ends with `macosx_12_0_x86_64.whl`
- **macOS Apple Silicon (12+)**: file name ends with `macosx_12_0_arm64.whl`

Put both wheels in one folder, then install from it, with no index:

{{< tabs "install-wheel">}}
{{< tab "Windows" >}}
```ps
py -m pip install --no-index --find-links ./wheels groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install --no-index --find-links ./wheels groupdocs-redaction-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install --no-index --find-links ./wheels groupdocs-redaction-net
```
{{< /tab >}}
{{< /tabs >}}

Expected output:

```bash
Looking in links: ./wheels
Processing ./wheels/groupdocs_redaction_net-26.11.0-py3-none-win_amd64.whl
Processing ./wheels/groupdocs_shared_net-26.11.0-py3-none-any.whl (from groupdocs-redaction-net)
Installing collected packages: groupdocs-shared-net, groupdocs-redaction-net
Successfully installed groupdocs-redaction-net-26.11.0 groupdocs-shared-net-26.11.0
```

Installing the product wheel alone, without `groupdocs_shared_net`, makes pip look for it on PyPI.

## Platform Prerequisites

Windows and macOS need nothing else. On Linux (Debian and Ubuntu shown), install ICU, which the .NET runtime needs to start, and fontconfig, which the presentation engine links (without it no PowerPoint or OpenDocument presentation opens):

```bash
sudo apt-get install libicu-dev libfontconfig1
```

For faithful rasterized output, also install the fonts your documents use, for example `ttf-mscorefonts-installer` for documents made with Microsoft Office. Without any font, text still renders, in a font the engine embeds. `libgdiplus` is not needed on any platform.

## Verify the Installation

Confirm the package imports and check the installed version:

```bash
python -c "import groupdocs.redaction; print('GroupDocs.Redaction is ready')"
```

You can also list the installed packages with `pip show groupdocs-redaction-net groupdocs-shared-net` to confirm the versions and location.

## Next Steps

- Follow the [Hello, World!]({{< ref "redaction/python-net/getting-started/hello-world.md" >}}) guide to run your first redaction.
- Read the [Features Overview]({{< ref "redaction/python-net/getting-started/features-overview.md" >}}) to see everything you can redact.
- Clone the [examples repository](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET) and read [How to Run Examples]({{< ref "redaction/python-net/getting-started/how-to-run-examples.md" >}}) to try every documented scenario locally.
