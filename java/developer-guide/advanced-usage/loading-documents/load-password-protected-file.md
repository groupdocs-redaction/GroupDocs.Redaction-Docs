---
id: load-password-protected-file
url: redaction/java/load-password-protected-file
title: Load password-protected file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Load password-protected file

In order to open password-protected documents, you have to pass your password to *LoadOptions* class constructor or assign it to its *Password* property of an instance of *LoadOptions* class:



```java
        LoadOptions loadOptions = new LoadOptions("mypassword");
        final Redactor redactor = new Redactor("protected_sample.docx", loadOptions);
        try 
        {
            // Here we can use document instance to perform redactions
            redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
            redactor.save();
        }
        finally { redactor.close(); }
```
