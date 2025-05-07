---
id: hello-world
url: redaction/python-net/hello-world
title: Hello, World!
second_title: Basic Example of Using GroupDocs.Redaction for Python via .NET
linkTitle: Hello World
weight: 2
keywords: "hello world, example, get started"
description: Quickly get started with GroupDocs.Redaction for Python via .NET by creating and running a simple example.
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

## Introduction
A "Hello, World!" example is often the first step when exploring GroupDocs.Redaction for Python via .NET. It serves as a simple test to confirm that your development environment is correctly set up and that the library is functioning as expected.

## Overview
"GroupDocs.Redaction for Python via .NET" allows you to search, redact, and remove sensitive information from various document formats. A wide range of [supported formats](/redaction/python-net/supported-document-formats/) makes it versatile for different use cases.

## How to Redact a Document Content
The following steps demonstrate how to redact sensitive information from a document using GroupDocs.Redaction for Python via .NET:

1. Import `groupDocs.redaction` classes.
2. Provide redaction parameters.
3. Instantiate a `Redactor` object with the path to the sample document.
4. Perform the required redaction operation.
5. Save the result document.

## Code Snippet
Basic example of GroupDocs.Redaction usage:

```python
import groupdocs.redaction as gr
import groupdocs.redaction.redactions as grr
from groupdocs.pydrawing import Color

def run():
    # Specify the redaction options
    color = Color.from_argb(128, 255, 0, 0)
    repl_o = grr.ReplacementOptions(color)
    ep_red = grr.ExactPhraseRedaction("John Doe", repl_o)

    # Load the document to be redacted
    with gr.Redactor("source.pdf") as redactor:

        # Apply the redaction
        result = redactor.apply(ep_red)
        
        # Save the redacted document
        redactor.save()
```
## Run the Application
Steps to run the sample application:
1. Download the Sample Application: 
    * [Download Samples Project](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET/)

2. Run the Application:
    * Navigate to the directory containing the `hello_world.py` script.
    * Run the script:
        ```bash 
        python hello_world.py
        ```

## Expected Output

![](/redaction/python-net/images/hello_word.png)

After executing the example, the resulting PDF file will have all instances of the text "John Doe" masked with small square images.

## Additional Resources
This demo application references the GroupDocs.Redaction for Python via .Net [code samples](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Python-via-.NET/).