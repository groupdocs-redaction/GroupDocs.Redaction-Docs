---
id: xls-spreadsheet-redactions
url: redaction/net/spreadsheet-redactions/xls-spreadsheet-redactions
title: XLS Spreadsheet redactions
weight: 8
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
GroupDocs.Redaction allows to remove sensitive or private data from your XLS spreadsheet document using specific filters, such as worksheet name/index or c column index.

## Redact specific XLS worksheet and column

In this example, we use both filters to redact a second column with emails on a worksheet "Customers", leaving untouched all other emails in the XLS document:

**C#**

```csharp
using (Redactor redactor = new Redactor("D:\\Sales in September.xls"))
{
   var filter = new CellFilter()
   {
      ColumnIndex = 1, // zero-based 2nd column
      WorkSheetName = "Customers"
   };
   var expression = new Regex("^\\w+([-+.']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$");
   RedactorChangeLog changeLog = redactor.Apply(new CellColumnRedaction(filter, expression, new ReplacementOptions("[customer email]")));
   if (result.Status != RedactionStatus.Failed)
   {
      doc.Save(new SaveOptions() { AddSuffix = true });
   };
}
```

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
