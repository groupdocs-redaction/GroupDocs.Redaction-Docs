---
id: save-with-default-options
url: redaction/nodejs-java/save-with-default-options
title: Save with default options
weight: 5
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The simplest way to save the document is to provide no parameters to Save method. In this case the document will be rasterized to PDF and will have the same name as the original one except its extension (.PDF). The PDF file will be overwritten.

The following example demonstrates usage of Save() method with default options.



{{< tabs "code-example-save-with-default-options" >}}
{{< tab "save_with_default_options.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
    // Save the document with default options (convert pages into images, save as PDF)
    redactor.save();
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/save-with-default-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/save-with-default-options/CodeExampleSaveWithDefaultOptions/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
