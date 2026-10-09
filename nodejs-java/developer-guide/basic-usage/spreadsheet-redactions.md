---
id: spreadsheet-redactions
url: redaction/nodejs-java/spreadsheet-redactions
title: Spreadsheet redactions
weight: 8
description: Redact sensitive data in spreadsheet formats including XLS, XLSX, XLSM, XLT, XLTX, XLTM, XLSB, ODS, OTS, CSV, TSV, and TAB.
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
GroupDocs.Redaction supports Microsoft Excel workbooks and templates (XLS, XLSX, XLSM, XLT, XLTX, XLTM, XLSB), OpenDocument spreadsheets (ODS, OTS), and text-based tables (CSV, TSV, TAB). See the full matrix in [Supported document formats]({{< ref "redaction/nodejs-java/getting-started/supported-document-formats.md" >}}).

DrawBox (colored rectangle) replacements are skipped for text-only formats such as CSV, TSV, and TAB — use a textual replacement string instead.

### Filter by spreadsheet and column

If you have a document with one or more tables, organized into worksheets (one table per worksheet) - such as Microsoft Excel documents - you can use specific type of textual redactions, *CellColumnRedaction*. It allows you to set the scope of the redaction to a specific worksheet and/or column. The options are:

*   optionally set worksheet name or its numeric index (if both are missing, redaction affects all worksheets)
*   optionally set column (all columns are used, if the column filter is not set)

If no filters are set, redactions affects the entire document. All indices are zero-based. Below is an example, where we use all filters, to redact second column with emails (e.g. loaded from database) on a worksheet "Customers", leaving untouched all other emails in the document:



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.xlsx');
try 
{
const filter = new redaction.CellFilter();
    filter.setColumnIndex(1);
    filter.setWorkSheetName('Customers');
const expression = Pattern.compile('^\\w+([-+.\']\\w+)*@\\w+([-.]\\w+)*\\.\\w+([-.]\\w+)*$');
const result = redactor.apply(new redaction.CellColumnRedaction(filter, expression, new redaction.ReplacementOptions('[customer email]')));
    if (result.getStatus() !== redaction.RedactionStatus.Failed)
    {
const so = new redaction.SaveOptions();
        so.setAddSuffix(true);
        so.setRasterizeToPDF(false);
        redactor.save(so);
    };
}
finally {
  redactor.close();
}
```
