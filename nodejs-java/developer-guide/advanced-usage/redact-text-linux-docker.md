---
id: redact-text-linux-docker
url: redaction/nodejs-java/redact-text-linux-docker
title: Redact text on Linux with Docker
weight: 9
description: Learn how to redact text in a PDF on Linux with Docker using GroupDocs.Redaction for Node.js via Java. Find an exact phrase and cover it with a black box.
keywords: linux, docker, text redaction, pdf, exact phrase, Node.js
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

You can use **GroupDocs.Redaction for Node.js via Java** to redact text from a PDF in a Linux Docker container. This tutorial shows how to create a Node.js application, find an exact phrase, cover it with a black box, and run the application in Docker. The same approach can be used with other [supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}).

## Create a Node.js project with Docker support

Create a Node.js project and add a Dockerfile to the project root.

```bash
mkdir PdfRedactionDocker
cd PdfRedactionDocker
npm init -y
```

The project layout is:

```text
PdfRedactionDocker/
├── Dockerfile
├── package.json
├── document.pdf
└── index.js
```

## Install GroupDocs.Redaction

Add **@groupdocs/groupdocs.redaction** to the project:

```bash
npm install @groupdocs/groupdocs.redaction@26.11.0
```

See [Installation]({{< ref "redaction/nodejs-java/getting-started/installation.md" >}}) for `JAVA_HOME` setup. The package provides the [Redactor](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/Redactor) class for loading and processing documents, along with the classes and options needed to find and redact sensitive content.

## Add the PDF file

Place the PDF you want to process in the project directory and name it `document.pdf`. The application searches this file for the target phrase and creates `document_Redacted.pdf` with the redacted content. In this example, the PDF contains the word `gap`.

## Add the redaction code

Replace the contents of `index.js` with the following code:

{{< tabs "code-example-redact-text-linux-docker" >}}
{{< tab "redact_text_linux_docker.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('document.pdf');
try {
  redactor.apply(new redaction.ExactPhraseRedaction('gap', new redaction.ReplacementOptions(Color.BLACK)));

  const saveOptions = new redaction.SaveOptions();
  saveOptions.setAddSuffix(true);
  redactor.save(saveOptions);
} finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "document.pdf" >}}
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/redact-text-linux-docker/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

[ExactPhraseRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ExactPhraseRedaction) searches the PDF for the specified phrase. The search is case-insensitive by default, so `gap` and `Gap` match the same text.

[ReplacementOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ReplacementOptions) with `Color.BLACK` covers each match with a black box instead of replacing the text with another string.

[SaveOptions.setAddSuffix(true)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) adds `_Redacted` to the file name, so the result is `document_Redacted.pdf`. The original `document.pdf` remains unchanged. See [Save in original format]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for other save options.

`apply` returns the redaction status. Check this status before treating the output as successfully redacted. `save` can still create an output file if the redaction was not applied.

## Configure the Dockerfile

The following Dockerfile installs Node.js, a JDK, fonts, and native build tools required by the `java` bridge, then installs npm dependencies.

**Dockerfile**

```dockerfile
FROM eclipse-temurin:17-jdk-jammy

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        curl \
        ca-certificates \
        fontconfig \
        fonts-dejavu-core \
        libfreetype6 \
        python3 \
        make \
        g++ \
    && curl -fsSL https://deb.nodesource.com/setup_20.x | bash - \
    && apt-get install -y --no-install-recommends nodejs \
    && fc-cache -f \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/opt/java/openjdk
ENV PATH="$JAVA_HOME/bin:$PATH"

WORKDIR /app
COPY package.json package-lock.json* ./
RUN npm install --omit=dev

COPY index.js ./

WORKDIR /data
ENTRYPOINT ["node", "/app/index.js"]
```

## Build the application image

From the project directory:

```bash
docker build -t PdfRedactionDocker .
```

## Run the container

Mount the project directory into the container and run the application:

```bash
docker run --rm \
  -v "${PWD}:/data" \
  -w /data \
  PdfRedactionDocker
```

The project directory is mounted at `/data` and used as the working directory. The application reads `/data/document.pdf` and writes `/data/document_Redacted.pdf`. Because `/data` is mapped to the project directory on the host, the redacted PDF appears next to the source file.

On Windows PowerShell, `${PWD}` expands to the current directory. Run the command from the project directory.

## Check the redacted PDF

Open `document_Redacted.pdf`. The specified phrase should be covered by a black rectangle, while the original `document.pdf` remains unchanged.

## More resources

* [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
* [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)

### Free online document redaction App

You can redact text and other sensitive content in PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, email files, and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
