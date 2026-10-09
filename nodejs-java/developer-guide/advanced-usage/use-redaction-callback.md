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
In order to reject specific changes during redaction process or to keep a full log of changes in the document, you need to set Redactor.RedactionCallback property, to a class implementing [IRedactionCallback](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction/IRedactionCallback) interface. The interface contains only one method, AcceptRedaction, which receives detailed information about proposed redaction and returns Boolean value, accepted or not.

Below, we create a callback with `java.extend`, dumping changes to the console:

```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');

const IRedactionCallback = java.import('com.groupdocs.redaction.IRedactionCallback');

const RedactionDump = java.extend(IRedactionCallback, {
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

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor(
  'Sample.docx',
  new redaction.LoadOptions(),
  new redaction.RedactorSettings(new RedactionDump()));
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```
