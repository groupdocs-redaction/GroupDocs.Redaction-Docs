---
id: save-in-rasterized-pdf
url: redaction/nodejs-java/save-in-rasterized-pdf
title: Save in rasterized PDF
weight: 2
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
The following example demonstrates how to save the document as a rasterized PDF file:

{{< tabs "code-example-save-in-rasterized-pdf" >}}
{{< tab "save_in_rasterized_pdf.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor(Constants.SAMPLE_DOCX);
try 
{
    // Here we can use document instance to perform redactions
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
const tmp0 = new redaction.SaveOptions();
    tmp0.setAddSuffix(false);
    tmp0.setRasterizeToPDF(true);
    // Saving as rasterized PDF with no suffix in file name
    redactor.save(tmp0);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/save-in-rasterized-pdf/CodeExampleSaveInRasterizedPdf/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
