---
id: use-redaction-policies
url: redaction/java/use-redaction-policies
title: Use redaction policies
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
If you have a corporate sensitive data removal policy as a list of redaction rules, you don't need to specify them in your code. You can specify an XML document with a list of pre-configured redactions.

Below is an example of redaction policy XML file (code properties mapping is obvious):

**RedactionPolicy.xml**

```java
<?xml version="1.0" encoding="utf-8"?>  
<redactionPolicy xmlns="http://www.groupdocs.com/redaction">  
  <regexRedaction regularExpression="(dolor)" actionType="ReplaceString" replacement="foobar" />  
  <exactPhraseRedaction searchPhrase="dolor" caseSensitive="true" actionType="DrawBox" color="Red" />   
  
  <cellColumnRedaction regularExpression="(foo)bar1" replacement="[red1]" columnIndex="1" worksheetIndex="2" /> 
  <cellColumnRedaction regularExpression="(foo)bar2" replacement="[red2]" wokrsheetName="Sample" /> 
  
  <eraseMetadataRedaction filter="All" />  
  <metadataSearchRedaction filter="Title, Author" replacement="foobar" valueExpression="(metasearch)" keyExpression="" />  
  
  <annotationRedaction regularExpression="(anno1)" replacement="foobar" />  
  <deleteAnnotationRedaction regularExpression="(anno2)" />  
  
  <imageAreaRedaction pointX="15" pointY="17" width="200" height="10" color="#AA50FC"  />  
  <imageAreaRedaction pointX="110" pointY="120" width="60" height="20" color="Magenta"  />  
</redactionPolicy> 
```
You can use RedactionPolicy.save() method to create XML documents of this structure, configuring redactions in runtime.

The following example demonstrates how to save a *RedactionPolicy* to an XML file.

{{< tabs "code-example-create-redaction-policy" >}}
{{< tab "create_redaction_policy.java" >}}
```java
RedactionPolicy policy = new RedactionPolicy(new Redaction[] {
    new ExactPhraseRedaction("Redaction", new ReplacementOptions("[Product]")),
    new RegexRedaction("\\d{2}\\s*\\d{2}[^\\d]*\\d{6}", new ReplacementOptions(java.awt.Color.BLUE)),
    new DeleteAnnotationRedaction(),
    new EraseMetadataRedaction(MetadataFilters.All)
});
policy.save("sample_policy.xml");
```
{{< /tab >}}
{{< /tabs >}}

You can have as much policies, as you need, loading them to redact your documents.

The example below loads a redaction policy from an XML file and applies every rule it contains to a document in a single `apply` call:



{{< tabs "code-example-use-redaction-policy" >}}
{{< tab "use_redaction_policy.java" >}}
```java
RedactionPolicy policy = RedactionPolicy.load("redaction_policy.xml");
final Redactor redactor = new Redactor("sample.docx");
try
{
    RedactorChangeLog result = redactor.apply(policy);
    if (result.getStatus() != RedactionStatus.Failed)
    {
        SaveOptions saveOptions = new SaveOptions();
        saveOptions.setAddSuffix(true);
        saveOptions.setRasterizeToPDF(false);
        saveOptions.setRedactedFileSuffix("redacted");
        redactor.save(saveOptions);
    }
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "redaction_policy.xml" >}}
{{< tab-text >}}
`redaction_policy.xml` is the policy file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/use-redaction-policies/redaction_policy.xml) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the document redacted in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/use-redaction-policies/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/use-redaction-policies/CodeExampleUseRedactionPolicy/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}
