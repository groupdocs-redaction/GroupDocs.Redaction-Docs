---
id: use-microsoft-azure-computer-vision
url: redaction/java/use-microsoft-azure-computer-vision
title: Use Microsoft Azure Computer Vision API 
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---

This implementation is based on [Microsoft Azure Computer Vision API](https://docs.microsoft.com/en-US/azure/cognitive-services/computer-vision/). The service is paid, but you can [create a free subscription](https://azure.microsoft.com/free/cognitive-services/). Once you've done with subscription, you will have to [create Computer Vision resource](https://portal.azure.com/#create/Microsoft.CognitiveServicesComputerVision) using the free pricing tier (F0) to try the service, and upgrade later to a paid tier for production. As a result, you will get Computer Vision Endpoint and Subscription Key (let's suppose they are stored in the environment variables COMPUTER_VISION_ENDPOINT and COMPUTER_VISION_SUBSCRIPTION_KEY respectively). 

**Java**

```java
import java.net.URI;
import java.io.InputStream;
import java.util.ArrayList;
import java.awt.Rectangle;
import java.security.SecureRandom;
import java.security.cert.CertificateException;
import java.security.cert.X509Certificate;
import javax.net.ssl.HostnameVerifier;
import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSession;
import javax.net.ssl.TrustManager;
import javax.net.ssl.X509TrustManager;

import org.apache.http.HttpEntity;
import org.apache.http.HttpResponse;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.entity.ContentType;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;
import org.apache.http.util.EntityUtils;
import org.apache.http.entity.InputStreamEntity;
import org.apache.http.conn.ssl.SSLConnectionSocketFactory;
import org.bouncycastle.util.Strings;
import org.json.JSONArray;
import org.json.JSONObject;

import com.groupdocs.redaction.integration.IOcrConnector;
import com.groupdocs.redaction.integration.RecognizedImage;
import com.groupdocs.redaction.integration.TextFragment;
import com.groupdocs.redaction.integration.TextLine;

public class MicrosoftAzureOcrConnector implements IOcrConnector
{
    private static final String OcrUri = "vision/v3.1/ocr";
    private final String getSubscriptionKey() { return System.getenv("COMPUTER_VISION_SUBSCRIPTION_KEY"); } 
    private final String getEndpoint() { return System.getenv("COMPUTER_VISION_ENDPOINT"); }
    private final String getUriBase() { return getEndpoint() + OcrUri; }

    public MicrosoftAzureOcrConnector()
    {
    }
    
    public final RecognizedImage recognize(InputStream imageStream)
    {
        try
        {
            SSLConnectionSocketFactory sslSocketFactory = createUnsecureSocketFactory();
            try (CloseableHttpClient httpClient = HttpClientBuilder.create().setSSLSocketFactory(sslSocketFactory).build())
            {
                URIBuilder uriBuilder = new URIBuilder(getUriBase());
                uriBuilder.setParameter("language", "unk");
                uriBuilder.setParameter("detectOrientation", "true");
                // Request parameters.
                URI uri = uriBuilder.build();
                HttpPost request = new HttpPost(uri);                 
                // Request headers.
                request.setHeader("Content-Type", "application/octet-stream");
                request.setHeader("Ocp-Apim-Subscription-Key", getSubscriptionKey());
                request.setHeader("Accept", "application/json");
                // Request body.              
                InputStreamEntity requestEntity = new InputStreamEntity(imageStream, ContentType.create("application/octet-stream"));
                request.setEntity(requestEntity);
                String stringResponse = null;
                try
                {
                    // Call the REST API method and get the response entity.
                    HttpResponse response = httpClient.execute(request);
                    HttpEntity entity = response.getEntity();
                    if (entity != null) 
                    {
                        // Format and display the JSON response.
                        stringResponse = EntityUtils.toString(entity);

                        System.out.println("REST Response:\n");
                        System.out.println(stringResponse);
                    }
                }
                catch (java.lang.Exception ex)
                {
                    // MS Azure Cognintive services reports 400 Bad requests and other exceptions on small pictures and pictures with no text
                    System.out.println("Microsoft Azure Cognitive Services consider this image as wrong: " + ex.toString());
                } 
                if (stringResponse != null) {
                    return createDtoFromResponse(new JSONObject(stringResponse));
                }
            }
        }
        catch (java.lang.Exception ex)
        {
            System.out.println("Microsoft Azure Cognitive Services Text Recognition failed: " + ex.toString());
        }
        return new RecognizedImage(new TextLine[0]);
    }

    private SSLConnectionSocketFactory createUnsecureSocketFactory() throws Exception
    {
        TrustManager[] trustAllCerts = new TrustManager[]{
            new X509TrustManager() 
            {
                public X509Certificate[] getAcceptedIssuers() {
                    return null;
                }

                public void checkServerTrusted(X509Certificate[] arg0, String arg1)
                        throws CertificateException {
                }

                public void checkClientTrusted(X509Certificate[] arg0, String arg1)
                        throws CertificateException {
                }
            }};
        SSLContext context = SSLContext.getInstance("TLS");
        context.init(null, trustAllCerts, new SecureRandom());            
        SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context,          
            new String[] { "TLSv1.2" },                                            
            null, 
            new HostnameVerifier() {
                @Override
                public boolean verify(String arg0, SSLSession arg1) {
                    return true;
                }
            });
        return sslSocketFactory;
    }

    private RecognizedImage createDtoFromResponse(JSONObject jToken)
    {
        // Parse json response to extract lines and words with the bounding rectangles.
    }

    ...
}
```
The service returns a JSON-serialized with text regions and recognized words, each word with its bounding rectangle.

You can find full implementation and an example of its usage here [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
