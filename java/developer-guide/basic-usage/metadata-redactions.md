---
id: metadata-redactions
url: redaction/java/metadata-redactions
title: Metadata redactions
weight: 6
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Filter metadata

Base functionality for all redactions, derived from MetadataRedaction base class is *metadata filtering* and it is mandatory for metadata redactions. It uses flagged enumeration *MetadataFilter*s, containing items for most frequent metadata entries. You can set the filter to *All*, or any combination of metadata. For instance, the example below sets filter to *Author*, *Manager* and *NameOfApplication* - for textual redaction or cleaning them out:



```java
// redaction derived from MetadataRedaction
redaction.setFilter(MetadataFilters.Author | MetadataFilters.Manager | MetadataFilters.NameOfApplication);
```

Below is the table with full list of *MetadataFilters* items:

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

### Clean metadata

You can replace all or specific metadata in the document with empty (blank or minimal) values. The example below blanks out all properties of the document:



```java
final Redactor redactor  = new Redactor("Sample.docx");
try 
{
    redactor.apply(new EraseMetadataRedaction(MetadataFilters.All));
    SaveOptions options = new  SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    // Save the document to "*_Redacted.*" file in original format
    redactor.save(options);
}
finally { redactor.close(); }
```

You can specify *MetadataFilter.All* or use default constructor to blank out all metadata within given document, Custom - to clear all custom metadata entries.

### Redact metadata

You can use *MetadataSearchRedaction* to remove sensitive data from document's metadata using regular expressions. For instance, we can remove any mention of "Company Ltd.":



```java
final Redactor redactor  = new Redactor("Sample.docx");
try 
{
    redactor.apply(new MetadataSearchRedaction("Company Ltd.", "--company--"));
    SaveOptions options = new SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    // Save the document to "*_Redacted.*" file in original format
    redactor.save(options);
}
finally { redactor.close(); }
```

First argument is regular expression, second is a replacement string. You can also set scope for redaction by setting filter, e.g. to *MetadataFilter.Company*. - it will leave the regular expressions matches undone in all metadata items, except "Company" property:



```java
final Redactor redactor  = new Redactor("Sample.docx");
try 
{
    MetadataSearchRedaction redaction = new MetadataSearchRedaction("Company Ltd.", "--company--");
    redaction.setFilter(MetadataFilters.Company);
    redactor.apply(redaction);
    SaveOptions options = new SaveOptions();
    options.setAddSuffix(true);
    options.setRasterizeToPDF(false);
    // Save the document to "*_Redacted.*" file in original format
    redactor.save(options);
}
finally { redactor.close(); }
```

### Metadata redaction status

All metadata redactions apply to each metadata item separately, and even if metadata item redaction fails, the rest of the metadata items will be updated. You can find a list of failed, skipped (rejected) metadata items and reasons for that in *ErrorMessage* property of *RedactorLogEntry.Result*.
