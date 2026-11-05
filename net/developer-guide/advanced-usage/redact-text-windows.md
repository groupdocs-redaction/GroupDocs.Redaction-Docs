---
id: redact-text-windows
url: redaction/net/redact-text-windows
title: Redact Text in a Word Document on Windows with GroupDocs.Redaction for .NET
weight: 10
description: Learn how to redact text in a Word document on Windows using GroupDocs.Redaction for .NET 26.10. Follow this .NET 10 tutorial to replace text matching a regular expression with a replacement string.
keywords: redact text in Word, Word document redaction, regex redaction, redact Word document on Windows, .NET 10, net10.0-windows, GroupDocs.Redaction
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

**GroupDocs.Redaction for .NET** lets you redact sensitive text in Word documents and other supported file formats. On Windows, you can use its Windows-specific build to integrate document redaction into Windows applications. This tutorial demonstrates how to create a .NET 10 console application targeting `net10.0-windows`, find a phrase in a Word document using a regular expression, replace the matching text, and save the redacted document. The same approach can be applied to other [supported document formats](/redaction/net/supported-document-formats/).

A complete working project is available in the [sample repository](https://github.com/groupdocs-redaction/sample-windows-specific-redaction).

## Create a .NET console project for Windows

Start by creating a .NET 10 console application in Visual Studio or with the .NET CLI. Set its target framework to `net10.0-windows` to use the Windows-specific build of GroupDocs.Redaction for .NET. NuGet automatically restores the `GroupDocs.Redaction.Net100.Windows` assembly for this target framework. It includes Windows-specific dependencies, such as `System.Drawing`.

If your application needs to run on multiple operating systems, use the cross-platform `net10.0` target framework instead. For details about supported platforms and framework requirements, see [System requirements](/redaction/net/system-requirements/) and [Migration notes](/redaction/net/migration-notes/).

### Using Visual Studio

Create a Console App and select .NET 10.0 as the target framework. After the project is created, open the project file and set:

```xml
<TargetFramework>net10.0-windows</TargetFramework>
```

### Using the .NET CLI

**bash**

```bash
dotnet new console -n WindowsSpecificRedaction -f net10.0
cd WindowsSpecificRedaction
```

Then set the same target framework in `WindowsSpecificRedaction.csproj`:

```xml
<TargetFramework>net10.0-windows</TargetFramework>
```

The project layout at this step is:

```text
WindowsSpecificRedaction/
├── WindowsSpecificRedaction.csproj
└── Program.cs
```

## Install GroupDocs.Redaction 26.10

Install **GroupDocs.Redaction for .NET 26.10.0** using Visual Studio or the .NET CLI. This package provides the APIs required to load documents, find text using regular expressions, apply redactions, and save the results.

In Visual Studio, open **Manage NuGet Packages**, search for `GroupDocs.Redaction`, and install version 26.10.0.

**bash**

```bash
dotnet add package GroupDocs.Redaction --version 26.10.0
```

The package provides the [Redactor](https://reference.groupdocs.com/net/redaction/groupdocs.redaction/redactor) class for loading and saving documents, [RegexRedaction](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.redactions/regexredaction) for applying redactions based on regular-expression matches, and [License.IsLicensed](https://reference.groupdocs.com/net/redaction/groupdocs.redaction/license) for checking whether a valid license is applied.

## Add the Word file

Place the Word document in the project directory and name it `document.docx`. Configure the project to copy the input file to the build output directory:

```xml
<ItemGroup>
  <None Update="document.docx">
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>
  </None>
</ItemGroup>
```

The sample document contains the phrase `essential tool`. The application finds this phrase, replaces the matching text, and creates a redacted output document. The original Word document remains unchanged.

## Add the redaction code

Replace the contents of `Program.cs` with the following code:

**C#**

```csharp
using GroupDocs.Redaction;
using GroupDocs.Redaction.Options;
using GroupDocs.Redaction.Redactions;
using System.Text.RegularExpressions;

var license = new License();
// license.SetLicense("your_license_path");

if (!license.IsLicensed)
{
    Console.WriteLine("The library is running in evaluation mode. Some limitations may apply.");
}

using (Redactor redactor = new Redactor("document.docx"))
{
    var regex = new Regex(@"\s+essential tool", RegexOptions.IgnoreCase);
    redactor.Apply(new RegexRedaction(regex, new ReplacementOptions(" [redacted]")));

    var saveOptions = new SaveOptions() { AddSuffix = true, RasterizeToPDF = false };
    var outputFile = redactor.Save(saveOptions);
}
```

[License.IsLicensed](https://reference.groupdocs.com/net/redaction/groupdocs.redaction/license) returns `false` until `SetLicense` loads a valid license. Uncomment `SetLicense` and provide the path to your license file to run the application with a valid license. Without a license, a single process can open up to 25 documents. Saved documents contain a trial badge at the top of each page. For more information, see [Evaluation limitations and licensing](/redaction/net/evaluation-limitations-and-licensing/).

The regular expression `\s+essential tool` matches one or more whitespace characters followed by `essential tool`. The search is case-insensitive, so `Essential Tool` also matches. Each match, including the whitespace before the phrase, is replaced with ` [redacted]`.

[SaveOptions.RasterizeToPDF](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.options/saveoptions) is set to `false`, so the document retains its original Word format. [SaveOptions.AddSuffix](https://reference.groupdocs.com/net/redaction/groupdocs.redaction.options/saveoptions) is set to `true`, so the output file is named `document_Redacted.docx`. See [Save in original format]({{< ref "redaction/net/developer-guide/advanced-usage/saving-documents/save-in-original-format.md" >}}) for more information about saving documents in their original formats.

`Apply` returns a `RedactorChangeLog` containing the redaction status. `Save` can still create an output file when the redaction was not applied.

## Run the application

### Using Visual Studio

Open `WindowsSpecificRedaction.slnx`, or open the project file. Press **F5** to debug or **Ctrl+F5** to run without debugging.

Visual Studio uses the output directory as the working directory. The redacted Word document is saved to `bin\Debug\net10.0-windows\document_Redacted.docx`.

### Using the .NET CLI

From the project directory:

**bash**

```bash
dotnet run
```

`dotnet run` uses the project directory as the working directory. The application reads `document.docx` from this directory and saves the redacted document as `document_Redacted.docx` alongside it.

## Check the redacted document

Open `document_Redacted.docx` to verify the result. The phrase `essential tool` should be replaced with `[redacted]`. The original `document.docx` remains unchanged.

You can adapt this example to redact other phrases, patterns, or sensitive text in Word documents by changing the regular expression and replacement text.

## More resources

Explore the following examples and documentation to learn more about document redaction with GroupDocs.Redaction. The GitHub projects provide sample applications for different platforms and programming languages.

You can run the complete sample to see how to redact Word document text using regular expressions and the Windows-specific build of GroupDocs.Redaction for .NET:

* [Redact a Word document on Windows](https://github.com/groupdocs-redaction/sample-windows-specific-redaction)
* [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
* [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
* [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)

### Free online document redaction App

You can also redact sensitive information without installing a library or writing code. GroupDocs provides a free online document redaction application for processing documents directly in your browser.

Use the [Free Online Document Redaction App](https://products.groupdocs.app/redaction) to find and redact text and other sensitive content in PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, email files, and other supported formats.