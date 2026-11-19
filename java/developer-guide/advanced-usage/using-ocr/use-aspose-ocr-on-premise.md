---
id: use-aspose-ocr-on-premise
url: redaction/java/use-aspose-ocr-on-premise
title: Use Aspose.OCR for Java on-premise API
weight: 4
description: "This article explains how to use Aspose.OCR for Java on-premise API with GroupDocs.Redaction."
keywords: Aspose.OCR for Java on-premise API
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---
This implementation is based on [Aspose.OCR for Java on-premise API](https://products.aspose.com/ocr/java/). Although it requires a valid license file, you can always request a temporary license for a month to evaluate.

Add the Aspose Maven repository and the `aspose-ocr` dependency to your project:

```xml
<repositories>
    <repository>
        <id>AsposeJavaAPI</id>
        <name>Aspose Java API</name>
        <url>https://releases.aspose.com/java/repo/</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>26.9.0</version>
    </dependency>
</dependencies>
```

**Java**

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.OcrInput;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.models.AreasType;
import com.aspose.ocr.models.DetectAreasMode;
import com.aspose.ocr.models.InputType;
import com.aspose.ocr.models.RectangleOutput;
import com.groupdocs.redaction.integration.ocr.IOcrConnector;
import com.groupdocs.redaction.integration.ocr.RecognizedImage;
import com.groupdocs.redaction.integration.ocr.TextFragment;
import com.groupdocs.redaction.integration.ocr.TextLine;

import javax.imageio.ImageIO;
import java.awt.Rectangle;
import java.awt.image.BufferedImage;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;

public class AsposeOCRStandaloneConnector implements IOcrConnector
{
    public AsposeOCRStandaloneConnector(String licenseFile) throws Exception
    {
        License lic = new License();
        lic.setLicense(licenseFile);
    }

    public RecognizedImage recognize(InputStream imageStream)
    {
        try
        {
            AsposeOCR api = new AsposeOCR();
            OcrInput ocrInput = new OcrInput(InputType.SingleImage);

            BufferedImage image = ImageIO.read(imageStream);
            ocrInput.add(image);

            RectangleOutput detectedRectangles = api.DetectRectangles(ocrInput, AreasType.LINES, false).get(0);

            RecognitionSettings recognitionSettings = new RecognitionSettings();
            recognitionSettings.setDetectAreasMode(DetectAreasMode.COMBINE);
            recognitionSettings.setRecognitionAreas(detectedRectangles.Rectangles);

            RecognitionResult result = api.Recognize(ocrInput, recognitionSettings).get(0);
            return createDtoFromResponse(result);
        }
        catch (Exception ex)
        {
            System.out.println("Aspose.OCR on-premise recognition failed: " + ex.toString());
        }
        return new RecognizedImage(new TextLine[0]);
    }

    protected RecognizedImage createDtoFromResponse(RecognitionResult result)
    {
        List<TextLine> lines = new ArrayList<TextLine>();
        for (RecognitionResult.LinesResult line : result.recognitionLinesResult)
        {
            String text = line.textInLine.trim();
            Rectangle rectangle = line.line;
            TextFragment fragment = new TextFragment(text, rectangle);
            lines.add(new TextLine(new TextFragment[] { fragment }));
        }
        return new RecognizedImage(lines.toArray(new TextLine[0]));
    }
}
```

First, identify rectangle areas of text using `DetectRectangles()` with `AreasType.LINES`. With this option you get a rectangle for every line of text. For word-level redaction, split each line into word fragments with their own rectangles before creating `TextFragment` instances.

Pass the connector to `RedactorSettings` when you open a document:

```java
RedactorSettings settings = new RedactorSettings(new AsposeOCRStandaloneConnector("Aspose.OCR.lic"));
final Redactor redactor = new Redactor("sample.docx", new LoadOptions(), settings);
try
{
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.BLACK)));
    redactor.save();
}
finally { redactor.close(); }
```

You can find related OCR examples here: [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java).

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Redaction for .NET examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-.NET)
    
*   [GroupDocs.Redaction for Java examples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java)
    

### Free online document redaction App

Along with full featured Java library we provide simple, but powerful free Apps.

You are welcome to perform redactions for various document formats like PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Redaction App](https://products.groupdocs.app/redaction).
