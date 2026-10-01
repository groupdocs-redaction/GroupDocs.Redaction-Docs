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

### Why To Migrate?

  
Here are the key reasons to use the new updated API provided by GroupDocs.Redaction for .NET since version 19.9:

*   **Redactor** class introduced as a **single entry point** to manage the document redaction process (instead of **Document**class from previous versions).
    
*   Methods **RedactWith()** of the **Document** class were replaced with similar **Apply()** methods in **Redactor** class.
    
*   Method **Document.Save(Stream, SaveOptions)** was replaced with **Redactor.Save(Stream, RasterizationOptions)**.
*   Constructor **LoadOptions(DocumentFormatConfiguration)** was removed.  
    
*   Exception and option classes were put in separate namespaces.   
    
*   **RedactionSummary** was renamed into **RedactorChangeLog**, **RedactionLogEntry** into **RedactorLogEntry**, **MetadataFilter** into **MetadataFilters**.  
    
*   Obsolete members were removed from Public API.
    
*   Added a number of new exception classes and base exception class for GroupDocs.Redaction exceptions.  
    

### How To Migrate?

The following example demonstrates how to redact Microsoft Office Word document and dumping statuses of applied redactions using old and new API:  

**Old coding style**

```csharp
using (Document doc = Redactor.Load(@"Documents/Doc/sample.docx"))
{
    // Here we can use document instance to perform redactions
	RedactionSummary summary = doc.RedactWith(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
	foreach (RedactionLogEntry entry in summary.RedactionLog)
	{
		Console.WriteLine(entry.Status.ToString());
	}
    doc.Save();
}
```

**New coding style**

```csharp
using (Redactor redactor = new Redactor(@"Documents/Doc/sample.docx"))
{
    // Here we can use document instance to perform redactions
    RedactorChangeLog result = redactor.Apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
	foreach (RedactorLogEntry entry in result.RedactionLog)
	{
		Console.WriteLine(entry.Status.ToString());
	}
	redactor.Save();
}
```

For more code examples and specific use cases please refer to our [Developer Guide]({{< ref "redaction/net/developer-guide/_index.md" >}}) documentation or [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET) samples and showcases.
