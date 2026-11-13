---
id: system-requirements
url: redaction/python-net/system-requirements
title: System Requirements
linkTitle: System Requirements
weight: 3
description: "GroupDocs.Redaction for Python via .NET ships as a self-contained wheel and runs on Windows, Linux, and macOS without Microsoft Office, OpenOffice, or any other third-party software installed."
keywords: System Requirements, supported operating systems, supported python versions, groupdocs redaction python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

{{< alert style="info" >}}
GroupDocs.Redaction for Python via .NET ships as a self-contained wheel that bundles the .NET runtime it needs. No Microsoft Office, Adobe Acrobat, third-party document software, .NET install or Mono install is required. On Linux two system packages are needed; see [Platform Dependencies](#platform-dependencies). To install the library, follow the steps in the [Installation]({{< ref "redaction/python-net/getting-started/installation.md" >}}) guide.
{{< /alert >}}

## Supported Operating Systems

GroupDocs.Redaction for Python via .NET runs on Windows, Linux, and macOS. The package ships as a platform-specific `.whl`, and `pip` picks the correct one automatically.

### Windows

* Microsoft Windows 10 (x64)
* Microsoft Windows 11 (x64)
* Microsoft Windows Server 2016, 2019, 2022 and 2025

The Windows wheel is 64-bit only: use a 64-bit Python.

### Linux

* Any **x86-64** distribution with **glibc 2.27 or newer** - for example Ubuntu 18.04+, Debian 10+, RHEL 8+. The embedded .NET runtime needs glibc 2.27, and the wheel's `manylinux_2_27_x86_64` tag says so, so pip refuses an older system.

### macOS

* macOS 12 (Monterey) and later - Intel and Apple Silicon (M-series). The wheels are tagged `macosx_12_0_*`, the oldest system the bundled .NET runtime starts on. Microsoft supports .NET 10 on macOS 14 and later.

## Python Version

GroupDocs.Redaction for Python via .NET supports **Python 3.5 through 3.14**, 64-bit. The wheel uses the `py3-none-{platform}` tag, meaning it works with any Python 3.x version in that range without per-version rebuilds.

| Python Version | Supported |
| --- | :---: |
| 3.5  | Yes |
| 3.6  | Yes |
| 3.7  | Yes |
| 3.8  | Yes |
| 3.9  | Yes |
| 3.10 | Yes |
| 3.11 | Yes |
| 3.12 | Yes |
| 3.13 | Yes |
| 3.14 | Yes |

## Package Manager

GroupDocs.Redaction for Python via .NET is distributed via [PyPI](https://pypi.org/project/groupdocs-redaction-net/) and the [GroupDocs Releases website](https://releases.groupdocs.com/redaction/python-net/):

```bash
pip install groupdocs-redaction-net
```

pip picks the wheel for your platform, and installs `groupdocs-shared-net` with it: the `groupdocs.pydrawing` and `groupdocs.pycore` modules that every GroupDocs product shares. To install without access to PyPI, download both wheels, as described on the [Installation]({{< ref "redaction/python-net/getting-started/installation.md" >}}) page. One wheel is published per platform:

| Platform | Wheel suffix |
| --- | --- |
| Windows 64-bit | `py3-none-win_amd64.whl` |
| Linux x64 (glibc) | `py3-none-manylinux_2_27_x86_64.whl` |
| macOS Apple Silicon | `py3-none-macosx_12_0_arm64.whl` |
| macOS Intel | `py3-none-macosx_12_0_x86_64.whl` |

`pip` 20.3 or newer picks the right wheel for your platform; older versions do not recognise these tags, so upgrade with `python -m pip install --upgrade pip` (on Python 3.5, `python -m pip install "pip==20.3.4"`). On an Intel Mac, a Python built against a pre-11 macOS SDK reports its system as macOS 10.16 - there use pip 24.1 or newer, or run `SYSTEM_VERSION_COMPAT=0 pip install groupdocs-redaction-net`.

## Platform Dependencies

### Linux

Install **ICU** and **fontconfig**:

```bash
sudo apt-get update
sudo apt-get install -y libicu-dev libfontconfig1
```

What each package is for, measured on the 26.10 engine with one document of each of the 41 formats on the [Supported Document Formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) page:

- **ICU** (`libicu-dev`, any version your distribution ships) - required. The .NET runtime needs it for text processing: without it, the first call into the engine aborts the Python process with `Couldn't find a valid ICU package`. Do not set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1` to work around it.
- **fontconfig** (`libfontconfig1`) - presentations. The presentation engine links it: without it, opening a PPTX, PPT, PPS, PPSX, PPSM, PPTM, POTX, POTM, ODP or OTP file raises `DllNotFoundException`. Every other format works without it.
- **Fonts** - the text of a rasterized PDF and of page previews is drawn in the fonts the document uses, as on Windows, so install them for faithful output (for example `ttf-mscorefonts-installer` from Debian's `contrib` section for documents made with Microsoft Office). With no font installed at all, text still renders, in a font the engine embeds, and the results of the format check were the same with only the DejaVu fonts as with the Microsoft core fonts.

`libgdiplus` is **not** needed: the engine draws with its own graphics library and ships no `System.Drawing.Common`.

The engine keeps a cache of the installed fonts in `~/.local/share/Aspose/Drawing/SystemFontCache.xml` (or under `$XDG_DATA_HOME`), and the package creates that folder when it is missing, as in a fresh container. Where it cannot be created (a read-only home), the engine writes the cache to `Aspose/Drawing/` in the working directory instead, once per process: set `XDG_DATA_HOME` to a writable folder.

### macOS

No extra dependencies - the wheel is self-contained. Its native libraries link only system frameworks.

### Windows

No extra dependencies - the wheel is self-contained.

## Development Environments

Any editor or IDE that runs CPython works, for example Visual Studio Code, PyCharm and Jupyter. Type stubs (`.pyi`) ship in the wheel, so editors complete class and member names.
