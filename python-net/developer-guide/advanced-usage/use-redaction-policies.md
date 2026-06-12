---
id: use-redaction-policies
url: redaction/python-net/use-redaction-policies
title: Use redaction policies
weight: 4
description: "Learn how to deal.If you have a corporate sensitive data removal policy as a list of redaction rules, you don't need to specify them in your code. You can specify an XML document with a list of pre-configured redactions."
keywords: list of pre-configured redactions
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
If you have a corporate sensitive data removal policy as a list of redaction rules, you don't need to specify them in your code. You can specify an XML document with a list of pre-configured redactions.

Below is an example of redaction policy XML file (code properties mapping is obvious):

**RedactionPolicy.xml**

```xml
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
 
{{< tabs "code-example-create-redaction-policy" >}}
{{< tab "create_redaction_policy.py" >}}
```python
from groupdocs.redaction import RedactionPolicy
from groupdocs.redaction.redactions import (
    ExactPhraseRedaction,
    ReplacementOptions,
    RegexRedaction,
    DeleteAnnotationRedaction,
    EraseMetadataRedaction,
    MetadataFilters,
)
from groupdocs.pydrawing import Color


def create_redaction_policy():
    # Define the color of redaction
    color = Color.from_argb(255, 220, 20, 60)

    # Configure the redactions
    redactions = [
        ExactPhraseRedaction("Redaction", ReplacementOptions("[Product]")),
        RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", ReplacementOptions(color)),
        DeleteAnnotationRedaction(),
        EraseMetadataRedaction(MetadataFilters.ALL),
    ]

    # Create the policy
    policy = RedactionPolicy(redactions)

    # Save the redaction policy to an XML file
    policy.save("./sample_policy.xml")
    print("Redactions policy saved to ./sample_policy.xml")


if __name__ == "__main__":
    create_redaction_policy()
```
{{< /tab >}}
{{< tab "sample_policy.xml" >}}  
```text
<?xml version="1.0"?>
<redactionPolicy>
  <exactPhraseRedaction actionType="ReplaceString" replacement="[Product]" searchPhrase="Redaction" />
  <regexRedaction actionType="DrawBox" color="#DC143C" regularExpression="\d{2}\s*\d{2}[^\d]*\d{6}" />
  <deleteAnnotationRedaction regularExpression="[.]*" />
  <eraseMetadataRedaction filter="All" />
</redactionPolicy>
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/use-redaction-policies/create_redaction_policy/sample_policy.xml)
{{< /tab >}}
{{< /tabs >}}

You can have as many policies as you need, loading them to redact your documents.

The example below loads a redaction policy from an XML file and applies every rule it contains to a document in a single `apply` call:

{{< tabs "code-example-use-redaction-policy" >}}
{{< tab "use_redaction_policy.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionPolicy
from groupdocs.redaction.options import SaveOptions

def use_redaction_policy():
    # Load the redaction policy from an XML file
    policy = RedactionPolicy.load("./redaction_policy.xml")

    # Load the document and apply the whole policy in one call
    with Redactor("./sample.docx") as redactor:
        redactor.apply(policy)

        # Keep the original format and append a suffix to the output name
        save_options = SaveOptions()
        save_options.add_suffix = True
        save_options.rasterize_to_pdf = False
        save_options.redacted_file_suffix = "redacted"
        result_path = redactor.save(save_options)

    print(f"Redaction policy applied. Output saved to {result_path}.")

if __name__ == "__main__":
    use_redaction_policy()
```
{{< /tab >}}
{{< tab "redaction_policy.xml" >}}
{{< tab-text >}}
`redaction_policy.xml` is the policy file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/use-redaction-policies/redaction_policy.xml) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the document redacted in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/use-redaction-policies/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/use-redaction-policies/use_redaction_policy/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}
