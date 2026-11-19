---
id: use-redaction-callback
url: redaction/nodejs-java/use-redaction-callback
title: Use redaction callback
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
In order to reject specific changes during redaction process or to keep a full log of changes in the document, you need to pass a callback implementing [IRedactionCallback](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/IRedactionCallback) into [RedactorSettings](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.options/RedactorSettings). The interface contains only one method, `acceptRedaction`, which receives detailed information about the proposed redaction and returns a Boolean value — accepted or not.

Below, we create a callback with `java.newProxy`, dumping changes to the console:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const callback = java.newProxy('com.groupdocs.redaction.redactions.IRedactionCallback', {
  acceptRedaction: function (description) {
    let message = description.getRedactionType() + ' redaction, '
      + description.getActionType() + ' action, item '
      + description.getOriginalText() + '. ';
    if (description.getReplacement() !== null) {
      message += 'Text ' + description.getReplacement().getOriginalText()
        + ' is replaced with ' + description.getReplacement().getReplacement() + '. ';
    }
    console.log(message);
    return true;
  }
});
```

The instance of this callback is passed to a constructor of the *Redactor* class:

{{< tabs "code-example-use-redaction-callback" >}}
{{< tab "use_redaction_callback.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor(
  'Sample.docx',
  new redaction.LoadOptions(),
  new redaction.RedactorSettings(callback));
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "Sample.docx" >}}
{{< tab-text >}}
`Sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/use-redaction-callback/Sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1012 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/use-redaction-callback/CodeExampleUseRedactionCallback/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
