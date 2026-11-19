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

Starting with GroupDocs.Redaction 26.11:

* Up to 25 documents can be opened in a single process. Attempting to open another document throws a `TrialLimitationsException`.
* Trial badges are added to the top of each page in the saved document.
* The previous limits of 1 document, 1 redaction, 4 replacements no longer apply.

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

## Check whether a license is applied

`License.isLicensed()` returns `true` when a valid license has been applied, and `false` when the component is running in evaluation mode.

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const license = new redaction.License();
license.setLicense('GroupDocs.Redaction.lic');

if (license.isLicensed()) {
  // licensed processing
}
```

Set the license once at application startup, before creating a `Redactor`.
