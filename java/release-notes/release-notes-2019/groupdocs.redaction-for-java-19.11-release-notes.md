---
id: groupdocs-redaction-for-java-19-11-release-notes
url: redaction/java/groupdocs-redaction-for-java-19-11-release-notes
title: GroupDocs.Redaction for Java 19.11 Release Notes
weight: 1
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 19.11.{{< /alert >}}

## Major Features

{{< alert style="danger" >}}In this version we're introducing new public API which was designed to be simple and easy to use. For more details about new API please check Public Docs section. The legacy API is no longer available.{{< /alert >}}

  
Other notable features:

*   Added support for Apple Numbers '09 spreadsheets
*   Added ability to specify PDF Compliance level

## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-47 | Add support for Apple Numbers format | Improvement |
| REDACTIONJAVA-48 | Add ability to specify PDF Compliance level | Improvement |

# Public API and Backward Incompatible Changes

Here are the key reasons to use the new updated API provided by GroupDocs.Redaction for Java since version 19.11:

*   **Redactor** class was introduced as a **single entry point** to manage the document redaction process (instead of **Document**class from previous versions).
    
*   Methods **redactWith()** of the **Document** class were replaced with similar **apply()** methods in **Redactor** class. 
    
*   Method **Document.save(OutputStream, SaveOptions)** was replaced with **Redactor.save(OutputStream, RasterizationOptions)**.
*   Constructor **LoadOptions(DocumentFormatConfiguration)** was removed.  
    
*   Exception and option classes were put in separate packages.   
    
*   **RedactionSummary** was renamed into **RedactorChangeLog**, **RedactionLogRecord** into **RedactorLogRecord**, **MetadataFilter** into **MetadataFilters**.  
    
*   Obsolete members were removed from public API.
    
*   Added a number of new exception classes and a base exception class for GroupDocs.Redaction exceptions.

##### Public API changes

Class **DocumentFormatException** has been moved to **com.groupdocs.redaction.exceptions**package.  
Class **IncorrectPasswordException** has been added to **com.groupdocs.redaction.exceptions**package.   
Class **PasswordRequiredException** has been added to **com.groupdocs.redaction.exceptions**package.   
Class **TrialLimitationsException** has been moved to**com.groupdocs.redaction.exceptions**package.  
Class **GroupDocsRedactionException** has been added to **com.groupdocs.redaction.exceptions**package.  
Class **LoadOptions** has been moved to **com.groupdocs.redaction.options**package.  
Class **RasterizationOptions** has been moved to **com.groupdocs.redaction.options**package.  
Class **Save****Options** has been moved to **com.groupdocs.redaction.options**package.  
Interface **ICreatePageStream** has been added to **com.groupdocs.redaction.options**package.  
Interface **IReleasePageStream** has been added to **com.groupdocs.redaction.options**package.  
Enum **PdfComplianceLevel** has been added to **com.groupdocs.redaction.options**package.  
Enum **PreviewFormats** has been added to **com.groupdocs.redaction.options**package.  
Class **PreviewOptions** has been added to **com.groupdocs.redaction.options**package.  
Interface **IPreviewable** has been added to **com.groupdocs.redaction.integration**package.  
Class **License** has been moved to **com.groupdocs.redaction.licensing**package.  
Class **Metered** has been moved to **com.groupdocs.redaction.licensing**package.  
Class **DocumentFormatConfiguration** has been moved to **com.groupdocs.redaction.configuration**package.  
Class **RedactorConfiguration** has been moved to **com.groupdocs.redaction.configuration**package.  
Class **DocumentFormatInstance** has been moved to **com.groupdocs.redaction.integration**package.  
Interface **IAnnotatedDocument** has been moved to **com.groupdocs.redaction.integration**package.  
Interface **ICellularFormatInstance** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **IImageFormatInstance** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **IMetadataAccess** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **IRasterizableDocument** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **ITextualFormatInstance** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **MetadataCollection** have been moved to **com.groupdocs.redaction.integration**package.  
Interface **MetadataItem** have been moved to **com.groupdocs.redaction.integration**package.  
Class **Document** has been removed from public API.  
Method **RedactorConfiguration.getInstance()** has been removed from public API.  
Method **getDefaultConfiguration()** has been added to**com.groupdocs.redaction.integration.DocumentFormatInstance** class.  
Method **getFormatConfiguration()** has been removed from **LoadOptions** class.  
Overloaded methods **redactWith(...)** of the **Document** class has been replaced with **apply(...)** methods of the**com.groupdocs.redaction.Redactor** class.  
Overloaded methods **d****etermineFormat(...)**  have been removed from public API.  
Obsolete method **getIsValidLicense()** has been removed from**GroupDocs.Redaction.License**class.  
Method **getDocumentInfo()**  has been added to **GroupDocs.Redaction.Redactor**class.  
Method **generatePreview(GroupDocs.Redaction.Options.PreviewOptions)** has been added to **GroupDocs.Redaction.Redactor**class.  
Methods **setAccessGranted(System.Boolean)** and **getAccessGranted()** have been added to **GroupDocs.Redaction.Integration.DocumentFormatInstance**class.  
Class **RedactionSummary**has been renamed into **RedactorChangeLog**.  
Class **RedactionLogEntry**has been renamed into **RedactorLogEntry**.  
Obsolete method **getSuccess()** has been removed from**GroupDocs.Redaction.RedactionResult**class.  
Obsolete method**getSuccess**() has been removed from**GroupDocs.Redaction.RedactorChangeLog**class.  
Flagged enumeration **MetadataFilter**has been renamed into **MetadataFilters**.  
Class **RedactionPolicy** has been moved to **com.groupdocs.redaction** package.  
Interface **IDocumentInfo**has been added to **com.groupdocs.redaction** package.  
Class **DocumentInfo** has been added to **com.groupdocs.redaction** package.  
Class **FileType**has been added to **com.groupdocs.redaction** package.  
Class **PageInfo**has been added to **com.groupdocs.redaction** package.  
Method **rasterize(OutputStream, RasterizationOptions)**  has been added to **com.groupdocs.redaction.integration.IRasterizableDocument**interface.

##### Usecases

The following example demonstrates how to redact Microsoft Office Word document and dumping statuses of applied redactions using old and new API:  

**Old coding style**

```java
// Load the file
Document doc = Redactor.load("Documents/Doc/sample.docx");
//Perform redaction using exact phrase
RedactionSummary summary = doc.redactWith(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[Personal]")));
for (RedactionLogEntry entry : summary.getRedactionLog())
{
	System.out.println(entry.getStatus());
}
//Save the resultant document
doc.save();
// Close the Document
doc.close();
```

**New coding style**

```java
// Load the file
Redactor redactor = new Redactor("Documents/Doc/sample.docx");
//Perform redaction using exact phrase
RedactorChangeLog summary = redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[Personal]")));
for (RedactorLogEntry entry : summary.getRedactionLog())
{
	System.out.println(entry.getResult().getStatus());
}
//Save the resultant document
redactor.save();
// Close the Redactor 
redactor.close();
```
