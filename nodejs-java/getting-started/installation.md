---
id: installation
url: redaction/nodejs-java/installation
title: Install GroupDocs.Redaction for Node.js via Java
linkTitle: Installation
weight: 4
description: "Install @groupdocs/groupdocs.redaction from npm, configure JAVA_HOME, and verify the bridge."
keywords: installation, npm, JAVA_HOME, Node.js via Java
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Prerequisites

- Node.js 20 LTS or later
- Java JRE/JDK 8+ (17 LTS recommended)
- Native build tools if required by `node-gyp` on your OS

See [System requirements]({{< ref "redaction/nodejs-java/getting-started/system-requirements.md" >}}).

### Install from npm

```bash
npm install @groupdocs/groupdocs.redaction
```

Or with yarn / pnpm:

```bash
yarn add @groupdocs/groupdocs.redaction
pnpm add @groupdocs/groupdocs.redaction
```

### Set up Java (`JAVA_HOME`)

Windows (PowerShell):

```powershell
$env:JAVA_HOME="C:\Program Files\Java\jdk-17"
$env:Path="$env:JAVA_HOME\bin;$env:Path"
```

Linux/macOS:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17
export PATH="$JAVA_HOME/bin:$PATH"
```

### Verify installation

```js
const redaction = require('@groupdocs/groupdocs.redaction');

try {
  console.log('Redactor:', typeof redaction.Redactor);
  console.log('GroupDocs.Redaction loaded successfully.');
  process.exit(0);
} catch (e) {
  console.error('Failed to load GroupDocs.Redaction:', e);
  process.exit(1);
}
```

Run with `node check.js`.

### Apply a license

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const license = new redaction.License();
license.setLicense('GroupDocs.Redaction.lic');
```

Without a license the evaluation limitations apply — see [Evaluation limitations and licensing]({{< ref "redaction/nodejs-java/getting-started/evaluation-limitations-and-licensing.md" >}}).
