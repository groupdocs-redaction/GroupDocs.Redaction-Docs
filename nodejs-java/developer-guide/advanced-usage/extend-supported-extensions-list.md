---
id: extend-supported-extensions-list
url: redaction/nodejs-java/extend-supported-extensions-list
title: Extend supported extensions list
weight: 5
description: "This article explains the method which can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured."
keywords: non-standard extensions
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
> **Note:** The samples on this page are Java classes from the GroupDocs.Redaction for Java API. Use them from Node.js via Java by placing the classes on the JVM classpath, or by wrapping the same interfaces with `java.extend`.


### Extend supported extensions list

This method can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured. For instance, all kinds of plain text files (batch, command files, etc.) could be opened. In this case you do not need to create your own format handler. As it is shown below, you can add file extension (e.g. ".dump") as being handled by the same *DocumentFormatInstance* as all plain text files:



```java
RedactorConfiguration config = DocumentFormatInstance.getDefaultConfiguration();
DocumentFormatConfiguration settings = config.findFormat(".txt");
settings.setExtensionFilter(docxSettings.getExtensionFilter() + ",.dump");
final Redactor redactor = new Redactor("C:\sample.dump");
try 
{
    // Here we can use the document instance to perform redactions
}
finally { redactor.close(); }
```

In detail, creating your own document format instances is covered in another article.
