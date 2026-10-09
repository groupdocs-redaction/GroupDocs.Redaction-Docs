---
id: system-requirements
url: redaction/nodejs-java/system-requirements
title: System requirements
weight: 3
description: "Node.js, Java, and OS requirements for GroupDocs.Redaction for Node.js via Java."
keywords: system requirements, Node.js, Java, JRE
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}
GroupDocs.Redaction for Node.js via Java works standalone and does not require Microsoft Office or Adobe Acrobat.
{{< /alert >}}

## Supported platforms

- Windows 10/11 and Windows Server 2016+
- Modern Linux distributions (x64)
- macOS 12+ (Intel and Apple Silicon, where Node.js and Java are available)

## Development environment

### Node.js

Node.js **20 LTS** or later (22 LTS supported).

### Java

JRE/JDK **8+** (11, 17, or 21 LTS recommended). Set `JAVA_HOME` so the Node–Java bridge can find the runtime.

### Native toolchain

The npm package depends on the [`java`](https://www.npmjs.com/package/java) bridge / `node-gyp`. Install OS build tools if npm install fails (see [node-gyp](https://www.npmjs.com/package/node-gyp) docs).

See [Installation]({{< ref "redaction/nodejs-java/getting-started/installation.md" >}}) for setup steps.
