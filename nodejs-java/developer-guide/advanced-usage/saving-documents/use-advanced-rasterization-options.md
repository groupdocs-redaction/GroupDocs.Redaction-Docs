---
id: use-advanced-rasterization-options
url: redaction/nodejs-java/use-advanced-rasterization-options
title: Use advanced rasterization options
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Node.js via Java
hideChildren: False
toc: True
---
### Use advanced rasterization options

In order to use the advanced rasterization options you have to pass one of the options to [Save](https://reference.groupdocs.com/java/redaction/groupdocs.redaction/redactor/methods/save) method. In this case the document will be rasterized to PDF, but the scan-like effects will be applied to its pages.

The following example demonstrates how to apply the [AdvancedRasterizationOptions](https://reference.groupdocs.com/redaction/java/groupdocs.redaction.options/advancedrasterizationoptions/) with default settings. 

{{< tabs "code-example-use-advanced-rasterization-options" >}}
{{< tab "use_advanced_rasterization_options.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.docx');
try 
{
    // Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
const so = new redaction.SaveOptions();
    so.setRedactedFileSuffix('_scan');
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt);
    redactor.save(so);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_scan.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/CodeExampleUseAdvancedRasterizationOptions/Sample_scan.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use border rasterization option

You can set the custom border width by providing the "border" dictionary item with an integer value.

The following example demonstrates how to apply the border advanced rasterization option with custom settings.

{{< tabs "code-example-use-border-rasterization-option" >}}
{{< tab "use_border_rasterization_option.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.docx');
try 
{
    // Save the document with a custom border
const so = new redaction.SaveOptions();
    so.setRedactedFileSuffix('_scan');
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border, new HashMap<String, String>() { { put('border', '10'); } });
    redactor.save(so);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_scan.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/CodeExampleUseBorderRasterizationOption/Sample_scan.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use grayscale rasterization option

The following example demonstrates how to apply the grayscale advanced rasterization option.

{{< tabs "code-example-use-grayscale-rasterization-option" >}}
{{< tab "use_grayscale_rasterization_option.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.docx');
try 
{
    // Save the document converting it to a grayscale
const so = new redaction.SaveOptions();
    so.setRedactedFileSuffix('_scan');
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    redactor.save(so);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_scan.pdf" >}}  
```text
Binary file (PDF, 975 KB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/CodeExampleUseGrayscaleRasterizationOption/Sample_scan.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use noise rasterization option

You can set up the custom noise effects by providing the "maxSpots" and "spotMaxSize" dictionary items having integer values. The "maxSpots" defines the maximal number of spots, which is random, and "spotMaxSize" defines the largest allowed spot size.

The following example demonstrates how to apply the noise advanced rasterization option with custom settings.

{{< tabs "code-example-use-noise-rasterization-option" >}}
{{< tab "use_noise_rasterization_option.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.docx');
try 
{
    // Save the document with the custom number and size of noise effects
const so = new redaction.SaveOptions();
    so.setRedactedFileSuffix('_scan');
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise, 
            new HashMap<String, String>() { { put('maxSpots', '150'); put('spotMaxSize', '15'); } });
    redactor.save(so);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_scan.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/CodeExampleUseNoiseRasterizationOption/Sample_scan.pdf)
{{< /tab >}}
{{< /tabs >}}

### Use tilt rasterization option

You can set up the custom tilt effects by providing the "minAngle" and "randomAngleMax" dictionary items having integer values. The "minAngle" defines the minimal rotation angle and "randomAngleMax" is a maximal rotation angle, randomly added to "minAngle".

The following example demonstrates how to apply the tilt advanced rasterization option with custom settings.

{{< tabs "code-example-use-tilt-rasterization-option" >}}
{{< tab "use_tilt_rasterization_option.js" >}}
```js
const redaction = require('@groupdocs/groupdocs.redaction');

const redactor = new redaction.Redactor('Sample.docx');
try 
{
    // Save the document with the custom tilt effect
const so = new redaction.SaveOptions();
    so.setRedactedFileSuffix('_scan');
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt,
            new HashMap<String, String>() { { put('minAngle', '85'); put('randomAngleMax', '5'); } });
    redactor.save(so);
}
finally {
  redactor.close();
}
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/nodejs-java/_sample_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "Sample_scan.pdf" >}}  
```text
Binary file (PDF, 1.1 MB)
```
[Download full output](/redaction/nodejs-java/_output_files/developer-guide/advanced-usage/saving-documents/use-advanced-rasterization-options/CodeExampleUseTiltRasterizationOption/Sample_scan.pdf)
{{< /tab >}}
{{< /tabs >}}

