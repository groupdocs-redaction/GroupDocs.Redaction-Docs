---
id: migration-notes
url: redaction/python-net/migration-notes
title: Migration Notes
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
### Why Migrate?  

Here are the key reasons to switch to the new, updated API provided by **GroupDocs.Redaction for Python via .NET** since version 19.9:

*   The **Redactor** class was introduced as a **single entry point** for managing the document redaction process (replacing the older **Document** class from previous versions).
    
*   The **RedactWith()** methods of the **Document** class were replaced with equivalent **apply()** methods in the **Redactor** class.
    
*   The method **Document.save(stream, save_options)** was replaced with **Redactor.save(stream, rasterization_options)**.
    
*   The constructor **LoadOptions(DocumentFormatConfiguration)** was removed.  
    
*   Exception and option classes were reorganized into separate namespaces.  
    
*   **RedactionSummary** was renamed to **RedactorChangeLog**, **RedactionLogEntry** to **RedactorLogEntry**, and **MetadataFilter** to **MetadataFilters**.  
    
*   Obsolete members were removed from the Public API.
    
*   A number of new exception classes were added along with a base exception class for GroupDocs.Redaction-specific exceptions.  


### How to Migrate?  

The following example demonstrates how to redact a Microsoft Word document and display the statuses of the applied redactions using the old and new APIs:  


```python
from groupdocs_redaction import Document, ExactPhraseRedaction, ReplacementOptions

# Load the document
with Document("sample.docx") as doc:
    # Apply redaction
    summary = doc.redact_with(ExactPhraseRedaction("John Doe", ReplacementOptions("[personal]")))

    # Display status of each redaction
    for entry in summary.redaction_log:
        print(entry.status)

    # Save the document
    doc.save()
