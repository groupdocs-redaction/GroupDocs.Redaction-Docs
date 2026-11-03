---
id: migration-notes
url: redaction/net/migration-notes
title: Migration Notes
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
### Migrate to version 26.10

#### Windows-specific builds

Version 26.10 introduces Windows-specific builds for .NET 6, .NET 8, and .NET 10.

Projects targeting `net6.0-windows`, `net8.0-windows`, or `net10.0-windows` benefit from improved compatibility with Windows applications because GroupDocs.Redaction uses Windows-specific dependencies, such as `System.Drawing`, for these target frameworks.

Projects targeting `net6.0`, `net8.0`, or `net10.0` retain the cross-platform implementation suitable for Linux. These builds do not depend on `System.Drawing.Common`.

Color, point, size, rectangle, and font values are still provided by `GroupDocs.Redaction.Options.Drawing` across all target frameworks.

#### Evaluation limits

Version 26.10 introduces updated evaluation mode limitations.

Without a license, a single process can open up to 25 documents. The previous limits of 1 document, 1 redaction, and 4 replacements no longer apply. Trial badges are still added to saved documents.


### Migrate to version 26.9

Cross-platform compatibility is improved by removing the dependency on `System.Drawing.Common`.

GroupDocs.Redaction now provides better support for Linux and other [Supported Operating Systems]({{< ref "redaction/net/getting-started/system-requirements.md#supported-operating-systems" >}}).

Version 26.9 removes `System.Drawing` types from the public API. Color, point, size, rectangle, and font values used by redactions now come from `GroupDocs.Redaction.Options.Drawing`.

Code that still passes `System.Drawing.Color`, `System.Drawing.Point`, `System.Drawing.Size`, `System.Drawing.Rectangle`, or `System.Drawing.Font` will no longer compile. Replace these arguments with the corresponding types from `GroupDocs.Redaction.Options.Drawing`:

```csharp
using GroupDocs.Redaction.Options.Drawing;

redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(Color.Black)));

redactor.Apply(new ImageAreaRedaction(
    new Point(516, 311),
    new RegionReplacementOptions(Color.Blue, new Size(170, 35))));
```

`Color` still exposes named colors (`Color.Black`, `Color.Blue`, and the other well-known names), `Color.FromName`, and `Color.FromArgb`.

Earlier 26.x builds kept the `System.Drawing` members and added temporary aliases that used the GroupDocs types. In 26.9 those aliases are obsolete. Use the original member names; they now use `GroupDocs.Redaction.Options.Drawing`:

| Obsolete alias | Use instead |
| --- | --- |
| `ReplacementOptions.BoxFillColor` | `ReplacementOptions.BoxColor` |
| `RegionReplacementOptions.AreaFillColor` | `RegionReplacementOptions.FillColor` |
| `RegionReplacementOptions.AreaSize` | `RegionReplacementOptions.Size` |
| `ImageAreaRedaction.TopLeftPosition` | `ImageAreaRedaction.TopLeft` |
| `PageAreaFilter.AreaRectangle` | `PageAreaFilter.Rectangle` |
| `TextFragment.BoundingRectangle` | `TextFragment.Rectangle` |

`IImageFormatInstance.EditArea` accepts `GroupDocs.Redaction.Options.Drawing.Point` only. `TextFragment` accepts `GroupDocs.Redaction.Options.Drawing.Rectangle` only. Map coordinates from an OCR engine into that rectangle before you create a fragment.

Packages for .NET 6, .NET 8, and .NET 10 no longer depend on `System.Drawing.Common`. Image-area redaction and PDF rasterization on those frameworks do not require GDI+ or `libgdiplus`. The .NET Framework 4.6.2 build still uses the Windows GDI+ stack.


For more code examples and specific use cases please refer to our [Developer Guide]({{< ref "redaction/net/developer-guide/_index.md" >}}) documentation or [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET) samples and showcases.
