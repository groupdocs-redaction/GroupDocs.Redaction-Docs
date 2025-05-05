---
id: use-aspose-ocr-on-premise
url: redaction/python-net/use-aspose-ocr-on-premise
title: Use Aspose.OCR for .NET on-premise API
weight: 4
description: "This article explains that how to use Aspose.OCR for .NET on-premise API."
keywords: Aspose.OCR for .NET on-premise API
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
This implementation is based on [Aspose.OCR for .NET on-premise API](https://products.aspose.com/ocr/python-net/). Although it requires a valid license file, you can always request a temporal license for a month to evaluate.

**C#**
```csharp
    using GroupDocs.Redaction.Integration.Ocr;

    public class AsposeOCRStandaloneConnector : IOcrConnector
    {
        public AsposeOCRStandaloneConnector(string licenseFile)
        {
            var lic = new Aspose.OCR.License();
            lic.SetLicense(licenseFile);
        }

        public RecognizedImage Recognize(Stream imageStream)
        {
            try
            {
                using (MemoryStream memStream = new MemoryStream())
                {
                    imageStream.CopyTo(memStream);
                    var api = new Aspose.OCR.AsposeOcr();
                    var rectangles = api.GetRectangles(memStream, Aspose.OCR.AreasType.LINES, false);
                    var result = api.RecognizeImage(memStream, new Aspose.OCR.RecognitionSettings()
                    {
                        Language = Aspose.OCR.Language.Eng,
                        RecognitionAreas = rectangles
                    });
                    return CreateDtoFromResponse(result);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Aspose.OCR for Cloud Recognition failed: {0}", ex.ToString());
            }
            return new RecognizedImage(new List<TextLine>());
        }

        protected virtual RecognizedImage CreateDtoFromResponse(Aspose.OCR.RecognitionResult result)
        {
            List<TextLine> lines = new List<TextLine>();
            for (int i = 0; i < result.RecognitionAreasText.Count; i++)
            {
                var fragments = RegularTextLine.SplitToFragments(result.RecognitionAreasText[i].Trim('\r', '\n'), result.RecognitionAreasRectangles[i]);
                lines.Add(new TextLine(fragments));
            }
            return new RecognizedImage(lines);
        }
    }

```

First, we identify rectangle areas of text using GetRectangles() method with Aspose.OCR.AreasType.LINES option. With this option, you will get a rectangle for every line of text, but you will have to split it to words.

You can find full implementation and an example of its usage here [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET).

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
