---
id: redact-text-linux-docker
url: redaction/net/redact-text-linux-docker
title: Redact text on Linux with Docker
weight: 9
description: Learn how to redact text in a PDF on Linux with Docker using GroupDocs.Redaction for .NET. Find an exact phrase and cover it with a black box in a .NET 10 application.
keywords: linux, docker, text redaction, pdf, exact phrase
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

You can use **GroupDocs.Redaction for .NET** to redact text from a PDF in a Linux Docker container. This tutorial shows how to create a .NET 10 console application, find an exact phrase, cover it with a black box, and run the application in Docker. The same approach can be used with other [supported document formats](/redaction/net/supported-document-formats/).

A complete working project is available in the [sample repository](https://github.com/groupdocs-redaction/sample-crossplatform-redaction-docker-linux).

## Create a .NET console project with Docker support

Create a .NET 10 console project in Visual Studio or with the .NET CLI.

### Using Visual Studio

Create a Console App and select .NET 10.0 as the target framework. On the additional options screen, enable **Enable container support** or **Add Docker support** (the option name depends on the Visual Studio version). Select Linux as the container operating system. Visual Studio creates the Docker configuration files, including a Dockerfile.

### Using the .NET CLI

**bash**

```bash
dotnet new console -n PdfRedactionDocker
cd PdfRedactionDocker
```

If you use the .NET CLI, add a Dockerfile to the project root manually. The following steps show how to configure it for a Linux container.

The project layout is:

```text
PdfRedactionDocker/
├── Dockerfile
├── PdfRedactionDocker.csproj
└── Program.cs
```

## Install GroupDocs.Redaction

Add **GroupDocs.Redaction for .NET** to the project with Visual Studio or the .NET CLI.

In Visual Studio, open **Manage NuGet Packages**, search for `GroupDocs.Redaction`, and install the package.

**bash**

```bash
dotnet add package GroupDocs.Redaction
```

The package provides the [Redactor](https://reference.groupdocs.com/net/redaction/groupdocs.redaction/redactor) class for loading and processing documents, along with the classes and options needed to find and redact sensitive content.

## Add the PDF file

Place the PDF you want to process in the project directory and name it `document.pdf`. The application searches this file for the target phrase and creates `document_Redacted.pdf` with the redacted content. In this example, the PDF contains the word `gap`.

## Add the redaction code

Replace the contents of `Program.cs` with the following code:

**C#**

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;
using GroupDocs.Redaction.Options.Drawing;
using GroupDocs.Redaction.Redactions;

using (Redactor redactor = new Redactor("document.pdf"))
{
    var status = redactor.Apply(
        new ExactPhraseRedaction(
            "gap",
            new ReplacementOptions(Color.Black)));

    var saveOptions = new SaveOptions() { AddSuffix = true };
    var outputFile = redactor.Save(saveOptions);
}
```

[ExactPhraseRedaction](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.redactions/exactphraseredaction) searches the PDF for the specified phrase. The search is case-insensitive by default, so `gap` and `Gap` match the same text.

[ReplacementOptions](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.redactions/replacementoptions) with [Color.Black](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.options.drawing/color) covers each match with a black box instead of replacing the text with another string.

[SaveOptions.AddSuffix](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.options/saveoptions) adds `_Redacted` to the file name, so the result is `document_Redacted.pdf`. The original `document.pdf` remains unchanged. See [Save in original format]({{< ref "redaction/net/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for other save options.

`Apply` returns the redaction status. Check this status before treating the output as successfully redacted. `Save` can still create an output file if the redaction was not applied.

## Configure the Dockerfile

The following Dockerfile installs the Linux libraries and fonts required by the sample for document processing. It is only the base stage, so it does not build or publish the .NET application. You can use it as a starting point or see the [complete Dockerfile](https://github.com/groupdocs-redaction/sample-crossplatform-redaction-docker-linux/blob/master/Dockerfile) in the sample repository.

**Dockerfile**

```dockerfile
FROM mcr.microsoft.com/dotnet/runtime:10.0 AS base

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        fontconfig \
        libfreetype6 \
        libgdiplus \
        libc6-dev \
        libx11-dev \
        software-properties-common \
    && echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
    && apt-add-repository multiverse \
    && apt-get update \
    && apt-get install -y ttf-mscorefonts-installer fonts-lato \
    && fc-cache -f \
    && dir="$(dirname "$(find /usr/lib /lib -name 'libdl.so.2' 2>/dev/null | head -n1)")" \
    && ln -sf "$dir/libdl.so.2" "$dir/libdl.so" \
    && rm -rf /var/lib/apt/lists/*

USER $APP_UID

WORKDIR /app
```

## Build the application image

Build the Docker image using the complete Dockerfile. The base stage shown above only prepares the Linux runtime and does not publish the application, so `/app/PdfRedactionDocker.dll` will not be in the image unless the Dockerfile also includes the build and publish stages.

In Visual Studio, select the Docker profile and start the project. Visual Studio builds the image and runs the application in the Linux container.

From the project directory:

**bash**

```bash
docker build -t PdfRedactionDocker .
```

## Run the container

Mount the project directory into the container and run the published .NET application:

**bash**

```bash
docker run --rm \
  -v "${PWD}:/data" \
  -w /data \
  --entrypoint dotnet \
  PdfRedactionDocker \
  /app/PdfRedactionDocker.dll
```

The project directory is mounted at `/data` and used as the working directory. The application reads `/data/document.pdf` and writes `/data/document_Redacted.pdf`. Because `/data` is mapped to the project directory on the host, the redacted PDF appears next to the source file.

On Windows PowerShell, `${PWD}` expands to the current directory. Run the command from the project directory.

## Check the redacted PDF

Open `document_Redacted.pdf`. The specified phrase should be covered by a black rectangle, while the original `document.pdf` remains unchanged.

## More resources

You can run the complete sample and see PDF text redaction in a Linux Docker container in our GitHub examples:

* [Redact text on Linux with Docker](https://github.com/groupdocs-redaction/sample-crossplatform-redaction-docker-linux)
* [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
* [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)

### Free online document redaction App

Along with the full-featured .NET library, we also provide free online apps for document redaction.

You can redact text and other sensitive content in PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, email files, and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
