---
id: use-pdf-redaction-filters
url: redaction/java/use-pdf-redaction-filters
title: Use PDF redaction filters
weight: 2
description: "Set page-level scope for redactions using PageRangeFilter and PageAreaFilter."
keywords: PageRangeFilter, PageAreaFilter, PDF page scope
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---

You can combine **PageRangeFilter** and **PageAreaFilter** in one set to limit a redaction to an area on a specific page (or slide). Assign the filters array to the **Filters** property of **ReplacementOptions**. The same approach applies to PDF and to other formats that support page filters.

The following example demonstrates how to apply redaction to the bottom half of the last page in a PDF document.

{{< tabs "code-example-use-pdf-redaction-filters" >}}
{{< tab "use_pdf_redaction_filters.java" >}}
```java
        final Redactor redactor = new Redactor("Sample.pdf");
        try 
        {
            // Get the actual size information for the last page:
            IDocumentInfo info = redactor.getDocumentInfo();
            PageInfo lastPage = info.getPages().get(info.getPageCount() - 1);
            ReplacementOptions options = new ReplacementOptions("[secret]");
            options.setFilters(new RedactionFilter[] {
                new PageRangeFilter(PageSeekOrigin.End, 0, 1),
                new PageAreaFilter(new java.awt.Point(0, lastPage.getHeight()/2),
                    new java.awt.Dimension(lastPage.getWidth(), lastPage.getHeight()/2))
            });
            RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("bibliography", false, options));
            if (result.getStatus() != RedactionStatus.Failed)
            {
                redactor.save();
            }                            
        }
        finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1018 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters/CodeExampleUsePdfRedactionFilters/Sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

