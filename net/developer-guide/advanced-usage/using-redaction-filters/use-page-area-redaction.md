---
id: use-page-area-redaction
url: redaction/net/use-page-area-redaction
title: Use PageAreaRedaction
weight: 3
description: "This article explains that how to use PageAreaRedaction."
keywords: free PDF page scope
productName: GroupDocs.Redaction for .NET
hideChildren: False
---

You can use [PageAreaRedaction](https://reference.groupdocs.com/redaction/net/groupdocs.redaction.redactions/pagearearedaction/) to redact an area of a specific page range from all sensitive data in text, images and annnotations.. 

The following example demonstrates how to apply PageAreaRedaction to the right half of the last page in a PDF document.

**C#**

```csharp
using GroupDocs.Redaction.Options.Drawing;

            using (Redactor redactor = new Redactor("Sample.pdf"))
            {
                Regex rx = new Regex("urna");
                ReplacementOptions optionsText = new ReplacementOptions("[redarea]");
                optionsText.Filters = new RedactionFilter[] {
                    new PageRangeFilter(PageSeekOrigin.End, 0, 1), // last page
                    //new PageAreaFilter(new System.Drawing.Point(300, 0), new System.Drawing.Size(300, 840)) // right half of the page 300x840
                    // Use GroupDocs.Redaction.Options.Drawing types instead of System.Drawing, which is scheduled for removal in future versions.
                    new PageAreaFilter(new Point(300, 0), new Size(300, 840)) // right half of the page 300x840
                };
                //RegionReplacementOptions optionsImg = new RegionReplacementOptions(System.Drawing.Color.Chocolate, new System.Drawing.Size(100, 100));
                // Use GroupDocs.Redaction.Options.Drawing types instead of System.Drawing, which is scheduled for removal in future versions.
                RegionReplacementOptions optionsImg = new RegionReplacementOptions(Color.Chocolate, new Size(100, 100));
                RedactorChangeLog result = redactor.Apply(new PageAreaRedaction(rx, optionsText, optionsImg));
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
