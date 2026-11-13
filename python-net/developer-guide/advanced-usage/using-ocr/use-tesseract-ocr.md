---
id: use-tesseract-ocr
url: redaction/python-net/use-tesseract-ocr
title: Use Tesseract OCR
weight: 2
description: "Redact text in scanned images with GroupDocs.Redaction for Python via .NET and an OCR connector built on the open-source Tesseract engine and pytesseract."
keywords: Tesseract, pytesseract, OCR, scanned document, IOcrConnector, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
[Tesseract](https://github.com/tesseract-ocr/tesseract) is an open-source OCR engine, and [pytesseract](https://pypi.org/project/pytesseract/) calls it from Python. This page builds an OCR connector on them (see [OCR usage basics]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-ocr/ocr-usage-basics.md" >}}) for what a connector is).

## Install Tesseract

Install the Tesseract program, then the two Python packages:

{{< tabs "tesseract-install" >}}
{{< tab "Linux" >}}
```bash
sudo apt-get install tesseract-ocr
pip install pytesseract pillow
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
brew install tesseract
pip install pytesseract pillow
```
{{< /tab >}}
{{< tab "Windows" >}}
```powershell
winget install UB-Mannheim.TesseractOCR
pip install pytesseract pillow
```
Add the Tesseract folder (`C:\Program Files\Tesseract-OCR`) to `PATH`, or set `pytesseract.pytesseract.tesseract_cmd` to the full path of `tesseract.exe`.
{{< /tab >}}
{{< /tabs >}}

## The connector

`pytesseract.image_to_data()` returns every word it recognized with its position and the block, paragraph and line it belongs to. The connector joins the words of each line into one `TextFragment` whose rectangle covers the line:

{{< tabs "code-example-use-tesseract-ocr" >}}
{{< tab "use_tesseract_ocr.py" >}}
```python
import io

import pytesseract
from PIL import Image

from groupdocs.redaction import Redactor
from groupdocs.redaction.integration.ocr import RecognizedImage, TextFragment, TextLine
from groupdocs.redaction.options import LoadOptions, RedactorSettings, SaveOptions
from groupdocs.redaction.options.drawing import Color, Rectangle
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions


class TesseractOcrConnector(object):
    """Recognizes text with Tesseract and reports each line as one fragment."""

    def recognize(self, image_stream):
        image = Image.open(io.BytesIO(image_stream.read()))
        data = pytesseract.image_to_data(image, output_type=pytesseract.Output.DICT)
        lines = {}
        order = []
        for i, word in enumerate(data["text"]):
            if not word.strip():
                continue
            key = (data["block_num"][i], data["par_num"][i], data["line_num"][i])
            if key not in lines:
                lines[key] = []
                order.append(key)
            lines[key].append(i)
        if not order:
            return None
        recognized = []
        for key in order:
            words = lines[key]
            left = min(data["left"][i] for i in words)
            top = min(data["top"][i] for i in words)
            right = max(data["left"][i] + data["width"][i] for i in words)
            bottom = max(data["top"][i] + data["height"][i] for i in words)
            text = " ".join(data["text"][i] for i in words)
            rectangle = Rectangle(left, top, right - left, bottom - top)
            recognized.append(TextLine([TextFragment(text, rectangle)]))
        return RecognizedImage(recognized)


def use_tesseract_ocr():
    settings = RedactorSettings(TesseractOcrConnector())
    with Redactor("./scan.png", LoadOptions(), settings) as redactor:
        result = redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions(Color.black)))
        print("Status: " + result.status.name)

        options = SaveOptions()
        options.add_suffix = True
        options.rasterize_to_pdf = False  # keep the PNG format
        result_path = redactor.save(options)
        print("Output saved to " + result_path)


if __name__ == "__main__":
    use_tesseract_ocr()
```
{{< /tab >}}
{{< tab "scan.png" >}}
{{< tab-text >}}
`scan.png` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/using-ocr/use-tesseract-ocr/scan.png) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "scan_Redacted.png" >}}  
```text
Binary file (PNG, 85 KB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/using-ocr/use-tesseract-ocr/use_tesseract_ocr/scan_Redacted.png)
{{< /tab >}}
{{< /tabs >}}

Each line is one fragment because GroupDocs.Redaction 26.10 covers a match inside a fragment and reports a match that spans two fragments as `APPLIED` without covering it. Inside a fragment, the box is placed by the match's character position, so near the end of a long line it can fall a few pixels short: on a 683-pixel line of text, the box over the last two words stopped 10 pixels before the last letter. On this page's sample, "Emily Johnson" in a 338-pixel line, the box covers the name. Check the output, or report shorter fragments, as long as each phrase you redact fits in one.

The same connector redacts the text of images embedded in a PDF or a Word document: open that document instead of the image.
