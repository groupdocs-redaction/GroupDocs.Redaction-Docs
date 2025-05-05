---
id: use-advanced-rasterization-options
url: redaction/python-net/use-advanced-rasterization-options
title: Use advanced rasterization options
weight: 7
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
## Use advanced rasterization options

In order to use the advanced rasterization options you have to pass one of the options to [Save](https://reference.groupdocs.com/python-net/redaction/groupdocs.redaction/redactor/methods/save) method. In this case the document will be rasterized to PDF, but the scan-like effects will be applied to its pages.

The following example demonstrates how to apply the [AdvancedRasterizationOptions](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.options/advancedrasterizationoptions/) with default settings. 

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Save the document with advanced options (convert pages into images, and save PDF with scan-like pages)
    var so = new SaveOptions();
    so.Rasterization.Enabled = true;
    so.RedactedFileSuffix = "_scan";
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Border);
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Noise);
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Tilt);
    redactor.Save(so);
}

```

### Use border rasterization option

You can set the custom border width by providing the "border" dictionary item with an integer value.

The following example demonstrates how to apply the border advanced rasterization option with custom settings.

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Save the document with a custom border
    var so = new SaveOptions();
    so.Rasterization.Enabled = true;
    so.RedactedFileSuffix = "_scan";
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Border, new Dictionary<string, string>() { { "border", "10" } });
    redactor.Save(so);
}

```

### Use grayscale rasterization option

The following example demonstrates how to apply the grayscale advanced rasterization option.

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Save the document with the custom grayscale effect
    var so = new SaveOptions();
    so.Rasterization.Enabled = true;
    so.RedactedFileSuffix = "_scan";
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Grayscale);
    redactor.Save(so);
}

```

### Use noise rasterization option

You can set up the custom noise effects by providing the "maxSpots" and "spotMaxSize" dictionary items having integer values. The "maxSpots" defines the maximal number of spots, which is random, and "spotMaxSize" defines the largest allowed spot size.

The following example demonstrates how to apply the noise advanced rasterization option with custom settings.

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Save the document with the custom number and size of noise effects
    var so = new SaveOptions();
    so.Rasterization.Enabled = true;
    so.RedactedFileSuffix = "_scan";
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Noise, 
                    new Dictionary<string, string>() { { "maxSpots", "150" }, { "spotMaxSize", "15" } });
    redactor.Save(so);
}

```

### Use tilt rasterization option

You can set up the custom tilt effects by providing the "minAngle" and "randomAngleMax" dictionary items having integer values. The "minAngle" defines the minimal rotation angle and "randomAngleMax" is a maximal rotation angle, randomly added to "minAngle".

The following example demonstrates how to apply the tilt advanced rasterization option with custom settings.

**C#**

```csharp
using (Redactor redactor = new Redactor(@"sample.docx"))
{
    // Save the document with the custom tilt effect
    var so = new SaveOptions();
    so.Rasterization.Enabled = true;
    so.RedactedFileSuffix = "_scan";
    so.Rasterization.AddAdvancedOption(AdvancedRasterizationOptions.Tilt,
                    new Dictionary<string, string>() { { "minAngle", "85" }, { "randomAngleMax", "5" } });
    redactor.Save(so);
}

```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
