---
id: redaction-basics
url: redaction/nodejs-java/redaction-basics
title: Redaction basics
weight: 4
description: "Redaction types and how to apply them with Redactor.apply in Node.js via Java."
keywords: apply redaction, RedactorChangeLog
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Redaction types

| Type | Description | Classes |
| --- | --- | --- |
| [Text]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/text-redactions.md" >}}) | Replace or hide text in the document body | `ExactPhraseRedaction`, `RegexRedaction` |
| [Metadata]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/metadata-redactions.md" >}}) | Erase or rewrite metadata | `EraseMetadataRedaction`, `MetadataSearchRedaction` |
| [Annotations]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/annotation-redactions.md" >}}) | Delete or rewrite annotations | `DeleteAnnotationRedaction`, `AnnotationRedaction` |
| [Images]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/image-redactions.md" >}}) | Cover an image area with a colored box | `ImageAreaRedaction` |
| [Pages]({{< ref "redaction/nodejs-java/developer-guide/basic-usage/remove-page-redactions.md" >}}) | Remove a page range | `RemovePageRedaction` |

### Apply redaction

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  const result = redactor.apply(
    new redaction.ExactPhraseRedaction('John Doe', new redaction.ReplacementOptions('[personal]')));
  if (result.getStatus() !== redaction.RedactionStatus.Failed) {
    redactor.save();
  }
} finally {
  redactor.close();
}
```

`apply` returns a `RedactorChangeLog`. Status values include `Applied`, `PartiallyApplied`, `Skipped`, and `Failed`.
