---
id: ocr-usage-basics
url: redaction/nodejs-java/ocr-usage-basics
title: OCR Usage Basics
weight: 2
description: "This article explains how to integrate any paid or free OCR solution with GroupDocs.Redaction for Node.js via Java."
keywords: free OCR solution
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---

Although GroupDocs.Redaction itself does not contain OCR as a part of its distributable, it allows you to integrate any paid or free OCR solution.
You have to implement [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface and its recognize() method, taking a stream with an image as an argument and returning a structured representation of the text, including bounding rectangles.

> **Note:** Connector implementations are Java classes (same contracts as GroupDocs.Redaction for Java). Provide them on the JVM classpath or wrap with `java.extend`, then pass the instance into `RedactorSettings` from Node.js.

**Java (connector skeleton)**

```java
public class MyOwnOcrConnector implements IOcrConnector
{
    public MyOwnOcrConnector()
    {
    }

    public RecognizedImage recognize(InputStream imageStream)
    {
	// TODO Create an instance of RecognizedImage class using OCR result returned by your OCR toolkit
    }
}
```

Once the instance is passed to [RedactorSettings](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/RedactorSettings) constructor, GroupDocs.Redaction will use it for image files and embedded images during an ordinary textual redaction process.

**Node.js**

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

// MyOwnOcrConnector is a Java class on the classpath (see skeleton above)
const redactor = new redaction.Redactor(
  'Sample.docx',
  new redaction.LoadOptions(),
  new redaction.RedactorSettings(new MyOwnOcrConnector()));
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions(Color.BLACK)));
  redactor.save();
} finally {
  redactor.close();
}
```

GroupDocs.Redaction provides two examples of the IOcrConnector implementation, free to use and customize for your needs. First, the [implementation based on Aspose.OCR for Cloud SDK]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-ocr/use-aspose-ocr-for-cloud" >}}). Second [implementation is using Microsoft Azure Cognitive Services API]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-ocr/use-microsoft-azure-computer-vision" >}}). Both services propose a trial subscription plan, but you can use any other free or paid OCR solution, web-based or on premise, by creating your own implementation of [IOcrConnector](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector).


## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
