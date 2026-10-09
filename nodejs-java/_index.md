---
id: home
url: redaction/nodejs-java
title: GroupDocs.Redaction for Node.js via Java
linkTitle: GroupDocs.Redaction for Node.js
weight: 1
description: "On-premise Node.js API to redact sensitive text, metadata, annotations, and image areas from PDF, Word, Excel, PowerPoint, and images. Requires a Java runtime."
keywords: redact PDF, Node.js redaction, GroupDocs.Redaction, Node.js via Java
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: True
fullWidth: True
---

<img src="/logo/128x128/groupdocs-redaction-java.png" alt="groupdocs-redaction-nodejs-java-home" align="left" style="width:110px; margin: 0 30px 30px 0"/>

{{< button style="primary" link="https://releases.groupdocs.com/redaction/nodejs-java/release-notes/" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#document"></use></svg> Release notes {{< /button >}}
{{< button style="primary" link="https://www.npmjs.com/package/@groupdocs/groupdocs.redaction" >}} {{< icon "gdoc_download" >}} Package repository {{< /button >}}

[GroupDocs.Redaction for Node.js via Java](https://products.groupdocs.com/redaction/) brings the GroupDocs.Redaction for Java API to Node.js so you can build on-premise apps that permanently remove or mask sensitive content without sending files to a third-party service.

Work with [PDF, Word, Excel, PowerPoint, images, and other supported formats]({{< ref "/redaction/nodejs-java/getting-started/supported-document-formats.md" >}}). Apply text, metadata, annotation, spreadsheet, and image-area redactions, optionally with page filters or OCR for text on images. Save in the original format or as a rasterized PDF when you need irreversible page images.

Install from npm (`@groupdocs/groupdocs.redaction`), point `JAVA_HOME` at a supported JDK, and call the same Java API surface from JavaScript.

<div style="clear:left"></div>

## Quick example

```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('sample.docx');
try {
  redactor.apply(new redaction.ExactPhraseRedaction(
    'John Doe',
    new redaction.ReplacementOptions('[personal]')));
  redactor.save();
} finally {
  redactor.close();
}
```

------

{{< columns >}}
<p><b>About GroupDocs.Redaction</b></p>
<hr><p>OVERVIEW</p></hr>
<ul>
    <li><a href='{{< ref "/redaction/nodejs-java/product-overview.md" >}}'>Product overview</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/features-overview.md" >}}'>Main features</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/supported-document-formats.md" >}}'>Supported file formats</a></li>
</ul>

<p>GET STARTED</p>
<ul>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/system-requirements.md" >}}'>System requirements</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/installation.md" >}}'>Installation</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/evaluation-limitations-and-licensing.md" >}}'>Licensing</a></li>
</ul>

<--->

<p><b>Developer Guide</b></p>
<hr><p>BASIC USAGE</p></hr>
<ul>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/redaction-basics.md" >}}'>Redaction basics</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/text-redactions.md" >}}'>Text redactions</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/metadata-redactions.md" >}}'>Metadata redactions</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/image-redactions.md" >}}'>Image redactions</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/annotation-redactions.md" >}}'>Annotation redactions</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/spreadsheet-redactions.md" >}}'>Spreadsheet redactions</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/basic-usage/remove-page-redactions.md" >}}'>Remove page redactions</a></li>
</ul>

<p>ADVANCED USAGE</p>
<ul>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/loading-documents/_index.md" >}}'>Loading documents</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/saving-documents/_index.md" >}}'>Saving documents</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/using-redaction-filters/_index.md" >}}'>Redaction filters</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/use-redaction-policies.md" >}}'>Redaction policies</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/using-ocr/_index.md" >}}'>Using OCR</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/use-redaction-callback.md" >}}'>Redaction callback</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/developer-guide/advanced-usage/saving-documents/save-word-with-ooxml-compliance.md" >}}'>OOXML compliance</a></li>
</ul>

<p>API REFERENCE</p>
<ul>
    <li><a href="https://reference.groupdocs.com/redaction/java/">GroupDocs.Redaction for Java API Reference</a></li>
</ul>

<--->

<p><b>Useful resources</b></p>
<hr><p>DEMOS AND EXAMPLES</p></hr>
<ul>
    <li><a href="https://products.groupdocs.app/redaction">Free online redaction app</a></li>
    <li><a href="https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java">Examples on GitHub (Java API map 1:1)</a></li>
    <li><a href='{{< ref "/redaction/nodejs-java/getting-started/how-to-run-examples.md" >}}'>How to run examples</a></li>
</ul>

<p>VERSION HISTORY</p>
<ul>
    <li><a href="https://releases.groupdocs.com/redaction/nodejs-java/release-notes/">GroupDocs.Redaction for Node.js via Java Release Notes</a></li>
</ul>

<p>TECHNICAL SUPPORT</p>
<ul>
    <li><a href="https://forum.groupdocs.com/c/redaction/33">Free support forum</a></li>
    <li><a href="https://helpdesk.groupdocs.com/">Paid support helpdesk</a></li>
    <li><a href="https://products.groupdocs.com/redaction/">Product page</a></li>
</ul>
{{< /columns >}}
