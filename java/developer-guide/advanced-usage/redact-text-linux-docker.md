---
id: redact-text-linux-docker
url: redaction/java/redact-text-linux-docker
title: Redact text on Linux with Docker
weight: 9
description: Learn how to redact text in a PDF on Linux with Docker using GroupDocs.Redaction for Java. Find an exact phrase and cover it with a black box.
keywords: linux, docker, text redaction, pdf, exact phrase, Java
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---

You can use **GroupDocs.Redaction for Java** to redact text from a PDF in a Linux Docker container. This tutorial shows how to create a Maven console application, find an exact phrase, cover it with a black box, and run the application in Docker. The same approach can be used with other [supported document formats]({{< ref "redaction/java/getting-started/supported-document-formats.md" >}}).

## Create a Java console project with Docker support

Create a Maven project that targets JDK 8 or later (JDK 17 LTS is recommended).

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=PdfRedactionDocker -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd PdfRedactionDocker
```

Add a Dockerfile to the project root. The project layout is:

```text
PdfRedactionDocker/
├── Dockerfile
├── pom.xml
├── document.pdf
└── src/main/java/com/example/App.java
```

## Install GroupDocs.Redaction

Add the GroupDocs repository and **GroupDocs.Redaction for Java** to `pom.xml`. See [Installation]({{< ref "redaction/java/getting-started/installation.md" >}}) for the current version and other build tools.

```xml
<repositories>
    <repository>
        <id>GroupDocs Artifact Repository</id>
        <name>GroupDocs Artifact Repository</name>
        <url>https://releases.groupdocs.com/java/repo/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-redaction</artifactId>
        <version>26.11</version>
    </dependency>
</dependencies>
```

The package provides the [Redactor](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/Redactor) class for loading and processing documents, along with the classes and options needed to find and redact sensitive content.

## Add the PDF file

Place the PDF you want to process in the project directory and name it `document.pdf`. The application searches this file for the target phrase and creates `document_Redacted.pdf` with the redacted content. In this example, the PDF contains the word `gap`.

## Add the redaction code

Replace the contents of `App.java` with the following code:

{{< tabs "code-example-redact-text-linux-docker" >}}
{{< tab "redact_text_linux_docker.java" >}}
```java
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.ExactPhraseRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

import java.awt.Color;

public class App {
    public static void main(String[] args) throws Exception {
        final Redactor redactor = new Redactor("document.pdf");
        try {
            redactor.apply(new ExactPhraseRedaction("gap", new ReplacementOptions(Color.BLACK)));

            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);
            redactor.save(saveOptions);
        } finally {
            redactor.close();
        }
    }
}
```
{{< /tab >}}
{{< tab "document.pdf" >}}
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/redact-text-linux-docker/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

[ExactPhraseRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ExactPhraseRedaction) searches the PDF for the specified phrase. The search is case-insensitive by default, so `gap` and `Gap` match the same text.

[ReplacementOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ReplacementOptions) with `Color.BLACK` covers each match with a black box instead of replacing the text with another string.

[SaveOptions.setAddSuffix(true)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) adds `_Redacted` to the file name, so the result is `document_Redacted.pdf`. The original `document.pdf` remains unchanged. See [Save in original format]({{< ref "redaction/java/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for other save options.

`apply` returns the redaction status. Check this status before treating the output as successfully redacted. `save` can still create an output file if the redaction was not applied.

## Configure the Dockerfile

The following Dockerfile installs the Linux libraries and fonts commonly required for document processing, builds the Maven project, and runs the application.

**Dockerfile**

```dockerfile
FROM eclipse-temurin:17-jdk-jammy AS build

WORKDIR /src
COPY pom.xml .
COPY src ./src
RUN apt-get update \
    && apt-get install -y --no-install-recommends maven \
    && mvn -q -DskipTests package \
    && rm -rf /var/lib/apt/lists/*

FROM eclipse-temurin:17-jre-jammy

USER root
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        fontconfig \
        fonts-dejavu-core \
        libfreetype6 \
    && fc-cache -f \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app
COPY --from=build /src/target/*.jar /app/app.jar

WORKDIR /data
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
```

Ensure `pom.xml` builds an executable JAR (for example with the Maven Shade Plugin or Spring Boot packaging), or adjust the `ENTRYPOINT` to run `java -cp ... com.example.App` with the GroupDocs dependency on the classpath.

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
