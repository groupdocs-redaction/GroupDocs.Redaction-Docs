---
id: use-redaction-policies
url: redaction/python-net/use-redaction-policies
title: Use redaction policies
weight: 4
description: "Learn how to deal.If you have a corporate sensitive data removal policy as a list of redaction rules, you don't need to specify them in your code. You can specify an XML document with a list of pre-configured redactions."
keywords: list of pre-configured redactions
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
---
If you have a corporate sensitive data removal policy as a list of redaction rules, you don't need to specify them in your code. You can specify an XML document with a list of pre-configured redactions.

Below is an example of redaction policy XML file (code properties mapping is obvious):

**RedactionPolicy.xml**

```python
<?xml version="1.0" encoding="utf-8"?>  
<redactionPolicy xmlns="http://www.groupdocs.com/redaction">  
  <regexRedaction regularExpression="(dolor)" actionType="ReplaceString" replacement="foobar" />  
  <exactPhraseRedaction searchPhrase="dolor" caseSensitive="true" actionType="DrawBox" color="Red" />   
  
  <eraseMetadataRedaction filter="All" />  
  <metadataSearchRedaction filter="Title, Author" replacement="foobar" valueExpression="(metasearch)" keyExpression="" />  
  
  <annotationRedaction regularExpression="(anno1)" replacement="foobar" />  
  <deleteAnnotationRedaction regularExpression="(anno2)" />  
  
  <imageAreaRedaction pointX="15" pointY="17" width="200" height="10" color="#AA50FC"  />  
  <imageAreaRedaction pointX="110" pointY="120" width="60" height="20" color="Magenta"  />  
</redactionPolicy> 
```
You can use RedactionPolicy.save() method to create XML documents of this structure, configuring redactions in runtime.

The following example demonstrates how to save a [RedactionPolicy](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/redactionpolicy/) to an XML file.
 
**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import groupdocs.pydrawing as grd

def run():
    # Define color of redaction
    color = grd.Color.from_argb(255, 220, 20, 60)

    # Configure Redactions
    redactions = [
        grr.ExactPhraseRedaction("Redaction", grr.ReplacementOptions("[Product]")),
        grr.RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", grr.ReplacementOptions(color)),
        grr.DeleteAnnotationRedaction(),
        grr.EraseMetadataRedaction(grr.MetadataFilters.ALL)
    ]

    # Create policy
    policy = gr.RedactionPolicy(redactions)

    # Save RedactionPolicy
    policy.save("sample_policy.xml")
```

You can have as much policies, as you need, loading them to redact your documents.

An example below shows how to apply redaction policy to all files within given inbound folder, and save to one of outbound folders - for successfully updated files and for failed ones. Current date and time is used as a part of output file name:

**Python**

```python
import groupdocs.redaction as gr
import groupdocs.redaction.options as gro
import groupdocs.redaction.redactions as grr
import os
from os.path import join

def run():

    # Initialize RedactionPolicy
    policy = gr.RedactionPolicy.load("sample_policy.xml")

    for file_entry in os.listdir("\inbound_dir"):
        cur_file = os.path.join("\inbound_dir", file_entry)

        # Load the document to be redacted
        with gr.Redactor(cur_file) as redactor:

            # Apply the redaction
            result = redactor.apply(policy)

            # Get output folder
            result_dir = "\out_bound_done_dir"
            if (result.status == gr.RedactionStatus.FAILED):
                result_dir = "\out_bound_failed_dir"

            output_file = join(result_dir, os.path.basename(cur_file))

            # Save file
            ro = gro.RasterizationOptions()
            ro.enabled = False
            with open(output_file, "wb") as stream_out:
                redactor.save(stream_out, ro)
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for Python via .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET)
*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
