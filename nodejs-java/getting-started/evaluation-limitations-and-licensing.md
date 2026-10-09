---
id: evaluation-limitations-and-licensing
url: redaction/nodejs-java/evaluation-limitations-and-licensing
title: Evaluation limitations and licensing
weight: 5
description: "Trial limits and how to apply a license for GroupDocs.Redaction for Node.js via Java."
keywords: license, trial, evaluation
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}You can use GroupDocs.Redaction without a license. Behavior matches the licensed API with evaluation limitations.{{< /alert >}}

## Evaluation limitations

* Only 1 document can be opened in one process.
* Only 1 redaction can be applied to the document.
* Any redaction is limited to 4 replacements/deletions, even if there are more matches.
* Trial badges are placed on the top of each page.

## Apply a license from a file

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const license = new redaction.License();
license.setLicense('GroupDocs.Redaction.lic');
```

## Apply a license from a stream

```js
const fs = require('fs');
const redaction = require('@groupdocs/groupdocs.redaction');

const stream = fs.createReadStream('GroupDocs.Redaction.lic');
const license = new redaction.License();
license.setLicense(stream);
```

Set the license once at application startup, before creating a `Redactor`.
