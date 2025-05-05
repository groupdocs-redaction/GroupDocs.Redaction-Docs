---
id: use-pdf-redaction-filters
url: redaction/python-net/use-pdf-redaction-filters
title: Use PDF redaction filters
weight: 2
description: "This article explains that how to set page-level scope to PDF redactions."
keywords: free PDF page scope
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

You can combine [PageRangeFilter](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/pagerangefilter/) and [PageAreaFilter](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/pageareafilter/) filters in one set in order to set the scope of redaction to an area on a specific page. You have to set an array of instances to **Filters** property of the [ReplacementOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/replacementoptions/). 

The following example demonstrates how to apply redaction to the bottom half of the last page in a PDF document.

**C#**

```csharp
using (Redactor redactor = new Redactor("Sample.pdf"))
{
    // Get the actual size information for the last page:
    IDocumentInfo info = redactor.GetDocumentInfo();
    PageInfo lastPage = info.Pages[info.PageCount - 1];
    ReplacementOptions options = new Redactions.ReplacementOptions("[secret]");
    options.Filters = new RedactionFilter[] {
        new PageRangeFilter(PageSeekOrigin.End, 0, 1),
        new PageAreaFilter(new System.Drawing.Point(0, lastPage.Height/2),
            new System.Drawing.Size(lastPage.Width, lastPage.Height/2))
    };
    RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("sample", false, options));
    if (result.Status != RedactionStatus.Failed)
    {
        redactor.Save();
    };
}

```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
