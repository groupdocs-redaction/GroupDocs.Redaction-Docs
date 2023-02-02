---
id: use-advanced-rasterization-options
url: redaction/java/use-advanced-rasterization-options
title: Use advanced rasterization options
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
### Use advanced rasterization options

In order to use the advanced rasterization options you have to pass one of the options to [Save](https://reference.groupdocs.com/java/redaction/groupdocs.redaction/redactor/methods/save) method. In this case the document will be rasterized to PDF, but the scan-like effects will be applied to its pages.

The following example demonstrates how to apply the [AdvancedRasterizationOptions](https://reference.groupdocs.com/redaction/java/groupdocs.redaction.options/advancedrasterizationoptions/) with default settings. 

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt);
    redactor.save(so);
}
finally { redactor.close(); }

```

### Use border rasterization option

You can set the custom border width by providing the "border" dictionary item with an integer value.

The following example demonstrates how to apply the border advanced rasterization option with custom settings.

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document with a custom border
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Border, new HashMap<String, String>() { { put("border", "10"); } });
    redactor.save(so);
}
finally { redactor.close(); }

```

### Use grayscale rasterization option

The following example demonstrates how to apply the grayscale advanced rasterization option.

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document converting it to a grayscale
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    redactor.save(so);
}
finally { redactor.close(); }

```

### Use noise rasterization option

You can set up the custom noise effects by providing the "maxSpots" and "spotMaxSize" dictionary items having integer values. The "maxSpots" defines the maximal number of spots, which is random, and "spotMaxSize" defines the largest allowed spot size.

The following example demonstrates how to apply the noise advanced rasterization option with custom settings.

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document with the custom number and size of noise effects
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Noise, 
            new HashMap<String, String>() { { put("maxSpots", "150"); put("spotMaxSize", "15"); } });
    redactor.save(so);
}
finally { redactor.close(); }

```

### Use tilt rasterization option

You can set up the custom tilt effects by providing the "minAngle" and "randomAngleMax" dictionary items having integer values. The "minAngle" defines the minimal rotation angle and "randomAngleMax" is a maximal rotation angle, randomly added to "minAngle".

The following example demonstrates how to apply the tilt advanced rasterization option with custom settings.

```java
final Redactor redactor = new Redactor("Sample.docx");
try 
{
    // Save the document with the custom tilt effect
    SaveOptions so = new SaveOptions();
    so.setRedactedFileSuffix("_scan");
    so.getRasterization().setEnabled(true);
    so.getRasterization().addAdvancedOption(AdvancedRasterizationOptions.Tilt,
            new HashMap<String, String>() { { put("minAngle", "85"); put("randomAngleMax", "5"); } });
    redactor.save(so);
}
finally { redactor.close(); }

```

