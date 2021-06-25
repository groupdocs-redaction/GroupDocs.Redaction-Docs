---
id: use-aspose-ocr-for-cloud
url: redaction/java/use-aspose-ocr-for-cloud
title: Use Aspose.OCR for Cloud SDK
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
This implementation is based on [Aspose.OCR for Cloud SDK](https://sdks.aspose.cloud/ocr/java/). Although it requires a valid Aspose.Cloud subscription, you can always [request a trial](https://dashboard.aspose.cloud/).

Let's suppose that the Aspose.Cloud AppSid and AppKey are stored in system environment variables ASPOSE_CLOUD_APPSID and ASPOSE_CLOUD_APPKEY. 

**Java**

```java
import java.io.IOException;
import java.io.InputStream;
import java.awt.Rectangle;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

import org.apache.commons.lang3.ArrayUtils;
import org.json.JSONArray;
import org.json.JSONObject;

import com.groupdocs.redaction.integration.RecognizedImage;
import com.groupdocs.redaction.integration.TextLine;
import com.groupdocs.redaction.integration.TextFragment;
import com.groupdocs.redaction.integration.IOcrConnector;

public class AsposeCloudOcrConnector implements IOcrConnector
{
    public AsposeCloudOcrConnector() 
    {
    }

    public RecognizedImage recognize(InputStream imageStream)
    {
        try
        {
            Configuration.setAPP_SID(System.getenv("ASPOSE_CLOUD_APPSID"));
            Configuration.setAPI_KEY(System.getenv("ASPOSE_CLOUD_APPKEY"));
            Configuration.setUserAgent("WebKit");
            
            final OcrApiInvoker api = new ApiClient().createService(OcrApiInvoker.class);            
            byte []payload = readBytes(imageStream);
            RequestBody requestBody = RequestBody.create( MediaType.parse("application/octet-stream"), payload);
            Call<ResponseBody> call = api.RecognizeFromContent(requestBody, Language.English, ResultType.Internal, 
                    DsrMode.DsrAndFilter, DsrConfidence.Default);
            Response<ResponseBody> res = call.execute();
            if (res.isSuccessful())
            {
                ResponseBody answer = res.body();
                JSONObject jToken = new JSONObject(answer.string());
                String result = jToken.getString("text");
                return createDtoFromResponse(new JSONObject(result));
            }
        }
        catch (java.lang.Exception ex)
        {
            throw new RuntimeException("Aspose.OCR for Cloud Recognition failed: " + ex.toString());
        }
        return new RecognizedImage(new TextLine[0]);
    }

    protected  RecognizedImage createDtoFromResponse(JSONObject jToken)
    {        
        // Recursively parse json tree with regions and text lines.
    }

    ...

}
```

The RecognizeFromContent() method with ResultType.Internal returns a JSON-serialized tree of text regions and recognized lines, with bounding rectangles. The text line is represented by a single object.

You can find full implementation and an example of its usage here [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
