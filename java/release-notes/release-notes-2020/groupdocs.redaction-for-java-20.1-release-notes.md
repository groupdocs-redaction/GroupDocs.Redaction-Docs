---
id: groupdocs-redaction-for-java-20-1-release-notes
url: redaction/java/groupdocs-redaction-for-java-20-1-release-notes
title: GroupDocs.Redaction for Java 20.1 Release Notes
weight: 12
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Redaction for Java 20.1{{< /alert >}}

## Major Features

There are the following improvements in this release:

*   Redactor settings including logging interface

## Full List of Issues Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| REDACTIONJAVA-61 | Implement standard logging interface | Improvement |

# Public API and Backward Incompatible Changes

### Implement standard logging interface

Implement standard logging interface for GroupDocs projects.

##### Public API changes   

Class **RedactorSettings** has been added to **com.groupdocs.redaction.options**package.  
Interface **ILogger** has been added to **com.groupdocs.redaction.options**package.  
Methods **Redactor.getRedactionCallback()** and **Redactor.setRedactionCallback(IRedactionCallback)** have been declared **deprecated**.  
Method **isRedactionAccepted(RedactionDescription)**  has been added to **com.groupdocs.redaction.integration.DocumentFormatInstance**class.  
Method **a****ddRange(MetadataCollection)**  has been added to **com.groupdocs.redaction.integration.MetadataCollection**class.  
Constructors, accepting an instance of **RedactorSettings** class have been added to **com.groupdocs.redaction.Redactor** class.  
Method **DocumentFormatInstance.initialize()** now requires an instance of**RedactorSettings** classas a second parameter.  
Method **String getDescription()** has been added to **com.groupdocs.redaction.Redaction** class.  
  

##### Usecases

The following example demonstrates how to set instances of **MyCustomLogger** and **MyRedactionCallback** classes:



```java
Redactor redactor = new Redactor("\\SampleFile.doc", new LoadOptions(), 
	new RedactorSettings(new MyCustomLogger(), new MyRedactionCallback())))
redactor.apply(new ExactPhraseRedaction("John Doe"), new ReplacementOptions(Color.RED));
redactor.save();
redactor.close();
```
