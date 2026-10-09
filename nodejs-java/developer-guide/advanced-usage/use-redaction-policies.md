---
id: use-redaction-policies
url: redaction/nodejs-java/use-redaction-policies
title: Use redaction policies
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
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

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const policy = new redaction.RedactionPolicy(java.newArray('com.groupdocs.redaction.Redaction', [
  new redaction.ExactPhraseRedaction('Redaction', new redaction.ReplacementOptions('[Product]')),
  new redaction.RegexRedaction('\\d{2}\\s*\\d{2}[^\\d]*\\d{6}', new redaction.ReplacementOptions(Color.BLUE)),
  new redaction.DeleteAnnotationRedaction(),
  new redaction.EraseMetadataRedaction(redaction.MetadataFilters.All)
]));
policy.save('MyPolicyFile.xml');
```

You can have as much policies, as you need, loading them to redact your documents.

An example below shows how to apply redaction policy to all files within given inbound folder, and save to one of outbound folders — for successfully updated files and for failed ones:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const fs = require('fs');
const path = require('path');
const FileOutputStream = java.import('java.io.FileOutputStream');

const policy = redaction.RedactionPolicy.load('Policy_file.xml');
const inbound = 'Inbound';
const files = fs.readdirSync(inbound)
  .map((name) => path.join(inbound, name))
  .filter((filePath) => fs.statSync(filePath).isFile());

for (const filePath of files) {
  const redactor = new redaction.Redactor(filePath);
  try {
    const result = redactor.apply(policy);
    const resultFolder = result.getStatus() !== redaction.RedactionStatus.Failed ? 'Done' : 'Failed';
    const fileName = path.basename(filePath);
    const fileStream = new FileOutputStream(path.join(resultFolder, fileName));
    try {
      const options = new redaction.RasterizationOptions();
      options.setEnabled(false);
      redactor.save(fileStream, options);
    } finally {
      fileStream.close();
    }
  } finally {
    redactor.close();
  }
}
```
