---
id: ocr-usage-basics
url: redaction/java/ocr-usage-basics
title: OCR Usage Basics
weight: 2
description:"This article explains that how to integrate any paid or free OCR solution in Java."
keywords: free OCR solution
productName: GroupDocs.Redaction for Java
hideChildren: False
---

Although GroupDocs.Redaction itself does not contain OCR as a part of its distributable, it allows you to integrate any paid or free OCR solution. 
You have to implement [IOcrConnector](https://apireference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector) interface and its recognize() method, taking a stream with an image as an argument and returning a structured representation of the text, including bounding rectangles. 

**Java**

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

Once the instance is passed to [RedactorSettings](https://apireference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/RedactorSettings) constructor, GroupDocs.Redaction will use it for image files and embedded images during an ordinary textual redaction process.

**Java**

```java
try (Redactor redactor = new Redactor("\\Sample.docx", new LoadOptions(), new RedactorSettings(new MyOwnOcrConnector())))
{
    // Assign an instance before using Redactor
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.BLACK)));
    redactor.save();
}

```

GroupDocs.Redaction provides two examples of the IOcrConnector implementation, free to use and customize for your needs. First, the [implementation based on Aspose.OCR for Cloud SDK]({{< ref "/redaction/java/developer-guide/advanced-usage/using-ocr/use-aspose-ocr-for-cloud" >}}). Second [implementation is using Microsoft Azure Cognitive Services API]({{< ref "/redaction/java/developer-guide/advanced-usage/using-ocr/use-microsoft-azure-computer-vision" >}}). Both services propose a trial subscription plan, but you can use any other free or paid OCR solution, web-based or on premise, by creating your own implementation of [IOcrConnector](https://apireference.groupdocs.com/redaction/java/com.groupdocs.redaction.integration/IOcrConnector).


## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
