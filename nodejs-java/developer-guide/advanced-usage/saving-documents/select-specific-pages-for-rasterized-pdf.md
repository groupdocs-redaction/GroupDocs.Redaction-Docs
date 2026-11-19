---
id: select-specific-pages-for-rasterized-pdf
url: redaction/nodejs-java/select-specific-pages-for-rasterized-pdf
title: Select specific pages for rasterized PDF
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Select specific pages for rasterized PDF

Saving document as a rasterized PDF, you can specify starting page index (zero based) and the number of pages from this index to save. Also, you can change the Compliance level from PDF/A-1b, which is used by default, to PDF/A-1a:



{{< tabs "code-example-select-specific-pages-for-rasterized-pdf" >}}
{{< tab "select_specific_pages_for_rasterized_pdf.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('MultipageSample.docx');
try 
{
const result = redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions(Color.RED)));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
const options = new redaction.SaveOptions();
        options.getRasterization().setEnabled(true);                           // the same as options.RasterizeToPDF = true;
        options.getRasterization().setPageIndex(5);                            // start from 6th page (index is 0-based)
        options.getRasterization().setPageCount(1);                            // save only one page
        options.getRasterization().setCompliance(PdfComplianceLevel.PdfA1a);   // by default PdfComplianceLevel.Auto or PDF/A-1b
        options.setAddSuffix(true);
        redactor.save(options);
    }
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "multipage_sample.docx" >}}
{{< tab-text >}}
`multipage_sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/select-specific-pages-for-rasterized-pdf/multipage_sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "MultipageSample_Redacted.pdf" >}}  
```text
Binary file (PDF, 10.7 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/select-specific-pages-for-rasterized-pdf/CodeExampleSelectSpecificPagesForRasterizedPdf/MultipageSample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
