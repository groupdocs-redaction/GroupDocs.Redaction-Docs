---
id: redact-text-windows
url: redaction/nodejs-java/redact-text-windows
title: Redact Text in a Document on Windows
weight: 10
description: Learn how to redact text in a Word document on Windows using GroupDocs.Redaction for Node.js via Java 26.11. Replace text matching a regular expression with a replacement string.
keywords: redact text in Word, Word document redaction, regex redaction, redact Word document on Windows, Node.js, GroupDocs.Redaction
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

**GroupDocs.Redaction for Node.js via Java** lets you redact sensitive text in Word documents and other supported file formats on Windows. This tutorial demonstrates how to create a Node.js application, find a phrase in a Word document using a regular expression, replace the matching text, and save the redacted document. The same approach can be applied to other [supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}).

## Create a Node.js project on Windows

Start with Node.js 20 LTS or later and a JDK 8+ installation (`JAVA_HOME` must be set). See [System requirements]({{< ref "redaction/nodejs-java/getting-started/system-requirements.md" >}}) for supported Windows versions.

```bash
mkdir WindowsSpecificRedaction
cd WindowsSpecificRedaction
npm init -y
```

The project layout at this step is:

```text
WindowsSpecificRedaction/
├── package.json
└── index.js
```

## Install GroupDocs.Redaction 26.11

Install **@groupdocs/groupdocs.redaction@26.11.0**. This package provides the APIs required to load documents, find text using regular expressions, apply redactions, and save the results.

```bash
npm install @groupdocs/groupdocs.redaction@26.11.0
```

See [Installation]({{< ref "redaction/nodejs-java/getting-started/installation.md" >}}) for `JAVA_HOME` setup and verification.

The package provides the [Redactor](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/Redactor) class for loading and saving documents, [RegexRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/RegexRedaction) for applying redactions based on regular-expression matches, and [License.isLicensed()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/License) for checking whether a valid license is applied.

## Add the Word file

Place the Word document in the project directory and name it `document.docx`. The sample document contains the phrase `essential tool`. The application finds this phrase, replaces the matching text, and creates a redacted output document. The original Word document remains unchanged.

## Add the redaction code

Replace the contents of `index.js` with the following code:

{{< tabs "code-example-redact-text-windows" >}}
{{< tab "redact_text_windows.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const license = new redaction.License();
// license.setLicense('your_license_path');

if (!license.isLicensed()) {
  console.log('The library is running in evaluation mode. Some limitations may apply.');
}

const redactor = new redaction.Redactor('document.docx');
try {
  redactor.apply(new redaction.RegexRedaction('\\s+essential tool', new redaction.ReplacementOptions(' [redacted]')));

  const saveOptions = new redaction.SaveOptions();
  saveOptions.setAddSuffix(true);
  saveOptions.setRasterizeToPDF(false);
  redactor.save(saveOptions);
} finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "document.docx" >}}
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/redact-text-windows/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

[License.isLicensed()](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/License) returns `false` until `setLicense` loads a valid license. Uncomment `setLicense` and provide the path to your license file to run the application with a valid license. Without a license, a single process can open up to 25 documents. Saved documents contain a trial badge at the top of each page. For more information, see [Evaluation limitations and licensing]({{< ref "redaction/nodejs-java/getting-started/evaluation-limitations-and-licensing.md" >}}).

The regular expression `\s+essential tool` matches one or more whitespace characters followed by `essential tool`. The search is case-insensitive by default, so `Essential Tool` also matches. Each match, including the whitespace before the phrase, is replaced with ` [redacted]`.

[SaveOptions.setRasterizeToPDF(false)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) keeps the document in its original Word format. [SaveOptions.setAddSuffix(true)](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/SaveOptions) names the output file `document_Redacted.docx`. See [Save in original format]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for more information about saving documents in their original formats.

`apply` returns a `RedactorChangeLog` containing the redaction status. `save` can still create an output file when the redaction was not applied.

## Run the application

From the project directory:

```bash
node index.js
```

The application reads `document.docx` from the working directory and saves the redacted document as `document_Redacted.docx` alongside it.

## Check the redacted document

Open `document_Redacted.docx` to verify the result. The phrase `essential tool` should be replaced with `[redacted]`. The original `document.docx` remains unchanged.

You can adapt this example to redact other phrases, patterns, or sensitive text in Word documents by changing the regular expression and replacement text.

## More resources

* [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
* [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)

### Free online document redaction App

Use the [Free Online Document Redaction App](https://products.groupdocs.app/redaction) to find and redact text and other sensitive content in PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, email files, and other supported formats.
