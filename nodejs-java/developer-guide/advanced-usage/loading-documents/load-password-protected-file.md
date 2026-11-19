---
id: load-password-protected-file
url: redaction/nodejs-java/load-password-protected-file
title: Load password-protected file
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Load password-protected file

In order to open password-protected documents, you have to pass your password to *LoadOptions* class constructor or assign it to its *Password* property of an instance of *LoadOptions* class:



{{< tabs "code-example-load-password-protected-file" >}}
{{< tab "load_password_protected_file.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const loadOptions = new redaction.LoadOptions('mypassword');
const redactor = new redaction.Redactor('protected_sample.docx', loadOptions);
        try 
        {
            // Here we can use document instance to perform redactions
            redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
            redactor.save();
        }
        finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "protected.docx" >}}
{{< tab-text >}}
`protected.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/protected.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "protected_sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/loading-documents/load-password-protected-file/CodeExampleLoadPasswordProtectedFile/protected_sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
