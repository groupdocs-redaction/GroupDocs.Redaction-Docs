---
id: text-redactions
url: redaction/nodejs-java/text-redactions
title: Text redactions
weight: 5
description: Apply text redaction with an exact phrase or regular expression to PDF, Word, Excel, PowerPoint, and other supported formats.
keywords: Node.js, redaction, ExactPhraseRedaction, RegexRedaction
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
You can redact text with [ExactPhraseRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ExactPhraseRedaction) or [RegexRedaction](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/RegexRedaction), using a replacement string or a colored box via [ReplacementOptions](https://reference.groupdocs.com/redaction/java/com.groupdocs.redaction.redactions/ReplacementOptions). To limit matches to a page range or area, set filters on `ReplacementOptions` (see [Using redaction filters]({{< ref "redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/_index.md" >}})).

### Use exact phrase redaction

In the example below, we apply textual redaction, replacing personal exact phrase "John Doe" with "\[personal\]" (or any exemption code):



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try 
{
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
    redactor.save();
}
finally {
  redactor.close();
}
```

By default, search for exact phase is case insensitive.For a case-sensitive redaction, there is a constructor parameter and corresponding public property:



```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try
{
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', true /*isCaseSensitive*/, new redaction.ReplacementOptions('[personal]')));
    redactor.save();
}
finally {
  redactor.close();
}
```

If you need a color box over the redacted text, you can use color instead of replacement string. The redaction will erase matched text and put a rectangle of the specified color in place of redacted text:



```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('sample.docx');
try
{
    redactor.apply(new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions(Color.RED)));
    redactor.save();
}
finally {
  redactor.close();
}
```

You might need to apply redaction to a right-to-left document, such as Arabic or Hebrew. The following example demonstrates how to apply ExactPhraseRedaction to an Arabic PDF document:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Arabic.pdf');
try
{
const red = new redaction.ExactPhraseRedaction('أﺑﺠﺪ', new redaction.ReplacementOptions('[test]'));
    red.setRightToLeft(true);
    redactor.apply(red);
    redactor.save();
}
finally {
  redactor.close();
}
```

### Use regular expression

Behind the scenes, "exact phrase" redaction works though regular expressions, which are the baseline approach for redaction. In the example below, we redact out any text, matching "2 digits, space or nothing, 2 digits, again space and 6 digits" with a blue color box:



```js
const redaction = require('@groupdocs/groupdocs.redaction');
const java = require('java');
const Color = java.import('java.awt.Color');

const redactor = new redaction.Redactor('sample.docx');
try
{
    redactor.apply(new redaction.RegexRedaction('\\d{2}\\s*\\d{2}[^\\d]*\\d{6}', new redaction.ReplacementOptions(Color.BLUE)));
const saveOptions = new redaction.SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    redactor.save(saveOptions);
}
finally {
  redactor.close();
}
```

If you need to apply redact a whole paragraph, you might also need to use RegexRedaction. The following example demonstrates how to redact the whole paragraph in a PDF document:

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('LoremIpsum.pdf');
try
{
    redactor.apply(new redaction.RegexRedaction('(Lorem(\n|.)+?urna)', new redaction.ReplacementOptions('[test]')));
const saveOptions = new redaction.SaveOptions();
    saveOptions.setAddSuffix(true);
    saveOptions.setRasterizeToPDF(false);
    redactor.save(saveOptions);
}
finally {
  redactor.close();
}
```
