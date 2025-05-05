---
id: use-aspose-ocr-for-cloud
url: redaction/python-net/use-aspose-ocr-for-cloud
title: Use Aspose.OCR for Cloud SDK
weight: 3
description: "This article explains that how to use Aspose.OCR for Cloud SDK."
keywords: 
productName: GroupDocs.Redaction for .NET
hideChildren: False
---
This implementation is based on [Aspose.OCR for Cloud SDK](https://products.aspose.cloud/ocr/python-net). Although it requires a valid Aspose.Cloud subscription, you can always [request a trial](https://dashboard.aspose.cloud/).

Let's suppose that the Aspose.Cloud AppSid and AppKey are stored in system environment variables ASPOSE_CLOUD_APPSID and ASPOSE_CLOUD_APPKEY. 

**C#**

```csharp
using Aspose.Ocr.Cloud.Sdk;
using Aspose.Ocr.Cloud.Sdk.Model;
using Aspose.Ocr.Cloud.Sdk.Model.Requests;
using Newtonsoft.Json.Linq;

public class AsposeOCRForCloudConnector : IOcrConnector
{
    private readonly Configuration configuration;

    public AsposeOCRForCloudConnector()
    {
        configuration = new Configuration();
        configuration.AppSid = Environment.GetEnvironmentVariable("ASPOSE_CLOUD_APPSID");
        configuration.AppKey = Environment.GetEnvironmentVariable("ASPOSE_CLOUD_APPKEY");
        configuration.ApiBaseUrl = "https://api.aspose.cloud";
        configuration.IdentityServerBaseUrl = "https://api.aspose.cloud";
    }

    public RecognizedImage Recognize(Stream imageStream)
    {
        try
        {
            OcrApi api = new OcrApi(configuration);
            var request = new PostOcrFromUrlOrContentRequest(imageStream, resultType: ResultType.Internal, dsrMode: DsrMode.DsrAndFilter);
            OCRResponse response = api.PostOcrFromUrlOrContent(request);
            return CreateDtoFromResponse(JToken.Parse(response.Text));
        }
        catch (Exception ex)
        {
            Console.WriteLine("Aspose.OCR for Cloud Recognition failed: {0}", ex.ToString());
        }
        return new RecognizedImage(new List<TextLine>());
    }

    protected virtual RecognizedImage CreateDtoFromResponse(JToken jToken)
    {
        return new RecognizedImage(LeafRecursion(jToken));
    }

    private TextLine[] LeafRecursion(JToken jToken)
    {
        List<TextLine> lines = new List<TextLine>();
        if (jToken["leaves"].Count() > 0)
        {
            foreach (var node in jToken["leaves"])
            {
                if (node["leaves"].Count() > 0)
                {
                    lines.AddRange(LeafRecursion(node));
                }
                else
                {
                    TextLine textLine = CreateTextLine(node);
                    if (textLine != null)
                    {
                        lines.Add(textLine);
                    }
                }
            }
        }
        return lines.ToArray();
    }

    private TextLine CreateTextLine(JToken line)
    {
        string lineText = line["values"].ToString();
        Rectangle lineRectangle = GetLineRectangle(line);
        if (!string.IsNullOrEmpty(lineText) && !lineRectangle.IsEmpty)
        {
            return new TextLine(RegularTextLine.SplitToFragments(lineText, lineRectangle));
        }
        else
        {
            return null;
        }
    }

    private Rectangle GetLineRectangle(JToken line)
    {
        var rect = line["rect"];
        return new Rectangle(rect[0].Value<int>(), rect[1].Value<int>(), rect[2].Value<int>() - rect[0].Value<int>(),
            rect[3].Value<int>() - rect[1].Value<int>());
    }
}

```

The PostOcrFromUrlOrContent() method with ResultType.Internal returns a JSON-serialized tree of text regions and recognized lines, with bounding rectangles. The text line is represented by a single object.

You can find full implementation and an example of its usage here [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET).

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
