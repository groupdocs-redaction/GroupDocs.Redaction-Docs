---
id: metadata-redactions
url: redaction/python-net/metadata-redactions
title: Metadata redactions
weight: 6
description: This article shows that how C# redaction API allows you to replace or remove metadata using filters or search by regular expression.
keywords: C#, redaction, api, remove metadata
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
With GroupDocs.Redaction API you can apply metadata redactions for documents of different formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX and others. See full list at [supported document formats]({{< ref "redaction/python-net/getting-started/supported-document-formats.md" >}}) article.

GroupDocs.Redactions provides a flexible API that allows to replace or remove metadata using filters or search by regular expression.

## Filter metadata

Base functionality for all redactions, derived from [MetadataRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadataredaction/) base class is *metadata filtering* and it is mandatory for metadata redactions. It uses flagged enumeration [MetadataFilters](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatafilters/), containing items for most frequent metadata entries. You can set the filter to *All*, or any combination of metadata. For instance, the example below sets filter to *Author*, *Manager* and *NameOfApplication* - for textual redaction or cleaning them out:

**Python**

```python
// redaction derived from MetadataRedaction
redaction.Filter = MetadataFilters.AUTHOR | MetadataFilters.MANAGER | MetadataFilters.NAME_OF_APPLICATION;
```

Below is the table with full list of [MetadataFilters](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatafilters/) items:

| Filter | Numeric value | Description |
| --- | --- | --- |
| *None* | 0 | Empty filter setting, matches no metadata items |
| *Author* | 1 | Author of the document |
| *Category* | 2 | Category of the document |
| *Comments* | 4 | Document comment |
| *Company* | 8 | Company of the Author |
| *ContentStatus* | 16 | Content status |
| *CreatedTime* | 32 | Created time |
| *HyperlinkBase* | 64 | Hyperlink base |
| *LastPrinted* | 128 | Last printed date and time |
| *LastSavedBy* | 256 | Last saved by user |
| *LastSavedTime* | 1024 | Last saved date and time |
| *NameOfApplication* | 2048 | Name of application where the document was created |
| *Manager* | 4096 | Author's manager name |
| *RevisionNumber* | 8192 | Revision number |
| *Subject* | 16384 | Subject of the document |
| *Template* | 32768 | Document template name |
| *Title* | 65536 | Document title |
| *TotalEditingTime* | 131072 | Total editing time |
| *Version* | 262144 | Document's version |
| *Description* | 524288 | Document's description |
| *Keywords* | 1048576 | Document's keywords |
| *ContentType* | 2097152 | Content type |
| *All* | 2147483647 | All types of the metadata items |

## Clean metadata

You can replace all or specific metadata in the document with empty (blank or minimal) values using [EraseMetadataRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/erasemetadataredaction/) class. The example below blanks out all properties of the document:

**Python**

```python
using (Redactor redactor = new Redactor(@"C:\sample.docx"))
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    met_red = grr.EraseMetadataRedaction(grr.MetadataFilters.ALL)

    # Load the document to be redacted
    with gr.Redactor("sample.docx") as redactor:

        # Apply the redaction
        result = redactor.apply(met_red)
        
        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
```

You can specify [MetadataFilter.All](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatafilters/) or use default constructor to blank out all metadata within given document, Custom - to clear all custom metadata entries.

## Redact metadata

You can use [MetadataSearchRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatasearchredaction/) to remove sensitive data from document's metadata using regular expressions. For instance, we can remove any mention of "Company Ltd.":

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    met_red = grr.MetadataSearchRedaction("Company Ltd.", "--company--")

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(met_red)
        
        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
```

First argument is regular expression, second is a replacement string. You can also set scope for redaction by setting filter, e.g. to [MetadataFilter.Company](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/metadatafilters/). - it will leave the regular expressions matches undone in all metadata items, except "Company" property:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr

def run():

    # Specify the redaction options
    met_red = grr.MetadataSearchRedaction("Company Ltd.", "--company--")
    met_red.filter = grr.MetadataFilters.COMPANY

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(met_red)
        
        # Save the redacted document
        so = gro.SaveOptions()
        so.add_suffix = True
        so.rasterize_to_pdf = False
        result_path = redactor.save(so)
```

## Metadata redaction status

All metadata redactions apply to each metadata item separately, and even if metadata item redaction fails, the rest of the metadata items will be updated. You can find a list of failed, skipped (rejected) metadata items and reasons for that in [ErrorMessage](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionresult/error_message/) property of [RedactorLogEntry.Result](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactorlogentry/result/).  
 

## More resources

### Advanced usage topics

To learn more about document redaction features, please refer to the [advanced usage section]({{< ref "redaction/python-net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
