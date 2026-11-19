---
id: extend-supported-extensions-list
url: redaction/java/extend-supported-extensions-list
title: Extend supported extensions list
weight: 5
description: "This article explains the method which can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured."
keywords: non-standard extensions
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
### Extend supported extensions list

This method can be used when for some reason files have non-standard extensions or if its format is supported, but not pre-configured. For instance, all kinds of plain text files (batch, command files, etc.) could be opened. In this case you do not need to create your own format handler. As it is shown below, you can add file extension (e.g. ".dump") as being handled by the same *DocumentFormatInstance* as all plain text files:



{{< tabs "code-example-extend-supported-extensions-list" >}}
{{< tab "extend_supported_extensions_list.java" >}}
```java
RedactorConfiguration config = DocumentFormatInstance.getDefaultConfiguration();
DocumentFormatConfiguration settings = config.findFormat(".txt");
settings.setExtensionFilter(settings.getExtensionFilter() + ",.dump");
final Redactor redactor = new Redactor("sample.dump");
try 
{
    // Here we can use the document instance to perform redactions
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.dump" >}}
{{< tab-text >}}
`sample.dump` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/extend-supported-extensions-list/sample.dump) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

In detail, creating your own document format instances is covered in another article.
