---
id: redact-text-windows
url: redaction/java/redact-text-windows
title: Redact Text in a Document on Windows
weight: 10
description: Learn how to redact text in a Word document on Windows using GroupDocs.Redaction for Java 26.11. Replace text matching a regular expression with a replacement string.
keywords: redact text in Word, Word document redaction, regex redaction, redact Word document on Windows, Java, GroupDocs.Redaction
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---

**GroupDocs.Redaction for Java** lets you redact sensitive text in Word documents and other supported file formats on Windows. This tutorial demonstrates how to create a Maven console application, find a phrase in a Word document using a regular expression, replace the matching text, and save the redacted document. The same approach can be applied to other [supported document formats]({{< ref "redaction/java/getting-started/supported-document-formats.md" >}}).

## Create a Java console project on Windows

Start by creating a Maven project that targets JDK 8 or later (JDK 17 LTS is recommended). See [System requirements]({{< ref "redaction/java/getting-started/system-requirements.md" >}}) for supported Windows versions and Java runtimes.

### Using the Maven CLI

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=WindowsSpecificRedaction -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
cd WindowsSpecificRedaction
```

The project layout at this step is:

```text
WindowsSpecificRedaction/
├── pom.xml
└── src/main/java/com/example/App.java
```

## Install GroupDocs.Redaction 26.11

Add the GroupDocs repository and **GroupDocs.Redaction for Java 26.11** to `pom.xml`. This package provides the APIs required to load documents, find text using regular expressions, apply redactions, and save the results.

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

See [Installation]({{< ref "redaction/java/getting-started/installation.md" >}}) for Gradle and other build tools.

The package provides the [Redactor](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/Redactor) class for loading and saving documents, [RegexRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/RegexRedaction) for applying redactions based on regular-expression matches, and [License.isLicensed()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/License) for checking whether a valid license is applied.

## Add the Word file

Place the Word document in the project directory and name it `document.docx`. The sample document contains the phrase `essential tool`. The application finds this phrase, replaces the matching text, and creates a redacted output document. The original Word document remains unchanged.

## Add the redaction code

Replace the contents of `App.java` with the following code:

{{< tabs "code-example-redact-text-windows" >}}
{{< tab "redact_text_windows.java" >}}
```java
import com.groupdocs.redaction.License;
import com.groupdocs.redaction.Redactor;
import com.groupdocs.redaction.options.SaveOptions;
import com.groupdocs.redaction.redactions.RegexRedaction;
import com.groupdocs.redaction.redactions.ReplacementOptions;

public class App {
    public static void main(String[] args) throws Exception {
        License license = new License();
        // license.setLicense("your_license_path");

        if (!license.isLicensed()) {
            System.out.println("The library is running in evaluation mode. Some limitations may apply.");
        }

        final Redactor redactor = new Redactor("document.docx");
        try {
            redactor.apply(new RegexRedaction("\\s+essential tool", new ReplacementOptions(" [redacted]")));

            SaveOptions saveOptions = new SaveOptions();
            saveOptions.setAddSuffix(true);
            saveOptions.setRasterizeToPDF(false);
            redactor.save(saveOptions);
        } finally {
            redactor.close();
        }
    }
}
```
{{< /tab >}}
{{< tab "document.docx" >}}
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/redact-text-windows/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

[License.isLicensed()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/License) returns `false` until `setLicense` loads a valid license. Uncomment `setLicense` and provide the path to your license file to run the application with a valid license. Without a license, a single process can open up to 25 documents. Saved documents contain a trial badge at the top of each page. For more information, see [Evaluation limitations and licensing]({{< ref "redaction/java/getting-started/evaluation-limitations-and-licensing.md" >}}).

The regular expression `\s+essential tool` matches one or more whitespace characters followed by `essential tool`. The search is case-insensitive by default, so `Essential Tool` also matches. Each match, including the whitespace before the phrase, is replaced with ` [redacted]`.

[SaveOptions.setRasterizeToPDF(false)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) keeps the document in its original Word format. [SaveOptions.setAddSuffix(true)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) names the output file `document_Redacted.docx`. See [Save in original format]({{< ref "redaction/java/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for more information about saving documents in their original formats.

`apply` returns a `RedactorChangeLog` containing the redaction status. `save` can still create an output file when the redaction was not applied.

## Run the application

From the project directory:

```bash
mvn -q compile exec:java -Dexec.mainClass=com.example.App
```

Or compile and run with your IDE. The application reads `document.docx` from the working directory and saves the redacted document as `document_Redacted.docx` alongside it.

## Check the redacted document

Open `document_Redacted.docx` to verify the result. The phrase `essential tool` should be replaced with `[redacted]`. The original `document.docx` remains unchanged.

You can adapt this example to redact other phrases, patterns, or sensitive text in Word documents by changing the regular expression and replacement text.

## More resources

* [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
* [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)

### Free online document redaction App

Use the [Free Online Document Redaction App](https://products.groupdocs.app/redaction) to find and redact text and other sensitive content in PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, email files, and other supported formats.
