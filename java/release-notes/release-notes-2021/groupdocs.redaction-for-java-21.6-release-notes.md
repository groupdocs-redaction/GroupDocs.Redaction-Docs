---
id: groupdocs-redaction-for-java-21-6-release-notes
url: redaction/java/groupdocs-redaction-for-java-21-6-release-notes
title: GroupDocs.Redaction for Java 21.6 Release Notes
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 21.6{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Enable OCR Processing  
    
## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-126 | Enable OCR Processing | Feature |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Redaction for Java 21.6. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Redaction which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Enable OCR Processing

This feature makes possible redaction of text in image documents and embedded images, using Optical Character Recognition (OCR) tools.

##### Public API changes
                                                                                            
Interface **IOcrConnector** providing methods that are required to apply textual redactions to image documents and embedded images has been **added**.  
Class **RecognizedImage** representing text, extracted from an image has been **added**.  
Class **TextLine** representing a line of text, extracted by OCR engine has been **added**.  
Class **TextFragment** representing a part of recognized text (word, symbol, etc) has been **added**.  
Class **RedactableImage** representing standalone or an embedded image has been **added**.  

##### Usage

The following example demonstrates how to use an implementation of **IOcrConnector** (e.g. **AsposeCloudOcrConnector** or any other OCR toolkit connector) to redact embedded images.
 
**Java**

```java
            RedactorSettings settings = new RedactorSettings(new MyOwnOcrConnector());
            try (Redactor redactor = new Redactor("FileWithEmbeddedImages.pdf", new LoadOptions(), settings))
            {
                ReplacementOptions marker = new ReplacementOptions(Color.BLACK);
                RedactorChangeLog result = redactor.apply(new Redaction[] {
                    new RegexRedaction("(?<=Dear\\s)([^,]+)", marker) // person name
                    new RegexRedaction("\\d{4}", marker)  // card number parts, etc
                });
                if (result.getStatus() != RedactionStatus.Failed)
                {
                    redactor.save(new SaveOptions(false, "Redacted"));
                }
            }
```



