---
id: groupdocs-redaction-for-java-20-11-release-notes
url: redaction/java/groupdocs-redaction-for-java-20-11-release-notes
title: GroupDocs.Redaction for Java 20.11 Release Notes
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 20.11{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Ability to save Redaction Policy to an XML file  
*   Built-in support for plain text format (previously was an example)  
*   Support for HTML documents and Markdown files  
*   Improve PDF preview generation  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-107 | Saving RedactionPolicy.xml file | Improvement |
| REDACTIONJAVA-108 | Add support for HTML documents and Markdown files | Improvement |
| REDACTIONJAVA-109 | Add built-in support for plain text format | Improvement |
| REDACTIONJAVA-110 | Improve PDF preview generation | Improvement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 20.11. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Saving RedactionPolicy.xml file in Java

This feature provides functionality to save a redaction policy created in code as an XML file for further use.

### Add support for HTML documents and Markdown files

This feature provides support for HTML documents and Markdown files.

### Add built-in support for plain text format

This feature provides built-in support for plain text format. Previously, user had to take the class from public examples and configure it as a custom format handler.

### Improve PDF preview generation

This feature contains improvements for PDF preview rendering and embedded images redactions.

##### Public API changes
                                                                                            
Constructor **RedactionPolicy(Redaction[])** taking an array of redactions has been **added**.  
Methods **RedactionPolicy.save(String)** and **RedactionPolicy.save(OutputStream)** have been **added**.  
Class **Redactor** now **implements** interface **IPreviewable**.  

##### Usage

The following example demonstrates how to save a *RedactionPolicy* to an XML file.

```java
RedactionPolicy policy = new RedactionPolicy(new Redaction[] {
    new ExactPhraseRedaction("Redaction", new ReplacementOptions("[Product]")),
    new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(java.awt.Color.BLUE)),
    new DeleteAnnotationRedaction(),
    new EraseMetadataRedaction(MetadataFilters.All)
});
policy.save("MyPolicyFile.xml");
```

The following example demonstrates how to get a single page preview of the document.

```java
// Test file
final String testFile = "D:\\sample.pdf";
// Take preview of the first page
int testPageNumber = 1;
// Preview file name
final String previewFileName = String.format("%s_page%d.png", testFile, testPageNumber);
// Load the document to generate preview
final Redactor redactor = new Redactor(testFile);
try 
{
    PreviewOptions options = new PreviewOptions(new ICreatePageStream() { 
        @Override
        public java.io.OutputStream createPageStream(int pageNumber) { 
            try {
                return new java.io.FileOutputStream(previewFileName); 
            } catch (java.io.FileNotFoundException ex) {
                System.out.printf("Failed to create preview file %s: \"%s\"\n\n", previewFileName, ex.toString());
                return null;
            }
        } 
    });
    options.setHeight(640);
    options.setWidth(480);
    options.setPageNumbers(new int[] { testPageNumber });
    options.setPreviewFormat(PreviewFormats.Png);
    redactor.generatePreview(options);            
    System.out.printf("\nPreview for page: %d  was saved to \"%s\"\n\n", testPageNumber, previewFileName);
}
finally { redactor.close(); }
```


