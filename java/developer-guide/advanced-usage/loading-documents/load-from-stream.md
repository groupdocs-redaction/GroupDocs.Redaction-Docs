---
id: load-from-stream
url: redaction/java/load-from-stream
title: Load from Stream
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Load from Stream

As an alternative to a local file, *Redactor* can open a document from stream.

The following example demonstrates how to load and redact a document using Stream:



```java
        final FileInputStream stream = new FileInputStream("sample.docx");
        try 
        {
            final Redactor redactor = new Redactor(stream);
            try 
            {
                // Here we can use document instance to make redactions
                redactor.apply(new DeleteAnnotationRedaction());
                redactor.save();
            }
            finally { redactor.close(); }
        }
        finally { stream.close(); }
```
