---
id: migration-notes
url: redaction/java/migration-notes
title: Migration Notes
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Why To Migrate?

  
Here are the key reasons to use the new updated API provided by GroupDocs.Redaction for Java since version 19.6:

*   **Redactor** class introduced as a **single entry point** to manage the document redaction process (instead of **Document**class from previous versions).
    
*   Methods **redactWith()** of the **Document** class were replaced with similar **apply()** methods in **Redactor** class.
    
*   Method **Document.save(OutputStream, SaveOptions)** was replaced with **Redactor.save(OutputStream, RasterizationOptions)**.
*   Constructor **LoadOptions(DocumentFormatConfiguration)** was removed.  
    
*   **RedactionSummary** was renamed into **RedactorChangeLog**, **RedactionLogRecord** into **RedactorLogRecord**, **MetadataFilter** into **MetadataFilters**.  
    
*   Obsolete members were removed from Public API.
    
*   Added a number of new exception classes and base exception class for GroupDocs.Redaction exceptions.  
    

### How To Migrate?

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

For more code examples and specific use cases please refer to our [Developer Guide]({{< ref "redaction/java/developer-guide/migration-notes.md" >}}) documentation or [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) samples and showcases.
