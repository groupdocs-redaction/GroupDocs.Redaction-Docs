---
id: product-overview
url: redaction/python-net/product-overview
title: GroupDocs.Redaction for Python via .NET Overview
linkTitle: Product overview
weight: 1
description: "GroupDocs.Redaction for Python via .NET removes or permanently obscures sensitive content — text, metadata, annotations, image areas, and whole pages — from PDF, DOCX, XLSX, PPTX, and images, entirely on-premise without Microsoft Office."
keywords: redaction, redact, remove sensitive information, PDF, DOCX, XLSX, PPTX, images, metadata, annotations, page removal, rasterized PDF, redaction policy, python, on-premise
productName: GroupDocs.Redaction for Python via .NET
toc: True
aliases:
  - /redaction/python-net/groupdocs.redaction-overview/
  - /redaction/python-net/groupdocs-redaction-overview/
---

## What is GroupDocs.Redaction?

GroupDocs.Redaction for Python via .NET is a native Python library that **permanently removes or obscures sensitive content** from documents — across PDF, Microsoft Word, Excel, PowerPoint, and image formats — through a single, format-independent API. It runs entirely on-premise, requires no Microsoft Office or Adobe Acrobat installation, and ships as a pre-built wheel on Windows, Linux, and macOS.

Typical uses include:

- **PII / PHI removal** — strip names, SSNs, emails, and other personal data from a document before it is shared, published, or archived (GDPR, HIPAA, CCPA).
- **Legal & e-discovery redaction** — black out privileged phrases and annotations across every page of a production set.
- **Metadata sanitization** — erase or rewrite author, company, and other hidden metadata that leaks information.
- **Irreversible redaction** — rasterize the cleaned document to a PDF so the removed content can never be recovered.
- **Policy-driven batch redaction** — define a reusable set of redaction rules once and apply it across many documents in a pipeline.

## Key Capabilities

| Capability | Description |
|---|---|
| **Text Redaction** | Replace or black out text matched by an exact phrase (case-sensitive or RTL-aware) or a regular expression. See [Text Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/text-redactions.md" >}}). |
| **Metadata Redaction** | Erase metadata wholesale or by filter, or rewrite values that match a pattern. See [Metadata Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/metadata-redactions.md" >}}). |
| **Image Redaction** | Black out a rectangular area of an image or scanned page and clean embedded image metadata. See [Image Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/image-redactions.md" >}}). |
| **Annotation Redaction** | Rewrite or delete annotations, comments, and notes by pattern. See [Annotation Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/annotation-redactions.md" >}}). |
| **Page Removal** | Remove whole pages, slides, or worksheets from a document. See [Remove Page Redactions]({{< ref "redaction/python-net/developer-guide/basic-usage/remove-page-redactions.md" >}}). |
| **Rasterization & Saving** | Save in the original format, or rasterize to a PDF (optionally PDF/A) so redactions are irreversible. See [Saving Documents]({{< ref "redaction/python-net/developer-guide/advanced-usage/saving-documents/_index.md" >}}). |
| **Redaction Policies** | Bundle several redactions into a reusable policy and apply it across many documents. See [Use Redaction Policies]({{< ref "redaction/python-net/developer-guide/advanced-usage/use-redaction-policies.md" >}}). |
| **Document Inspection** | Read file type, page count, and size without modifying the document. See [Get File Info]({{< ref "redaction/python-net/developer-guide/basic-usage/get-file-info.md" >}}). |

## Quick Example

Redact every occurrence of a phrase and save the result with just a few lines of code. The example rasterizes the result to a PDF named `sample_redacted.pdf`, so the removed content cannot be recovered:

{{< tabs "product-overview-redact-text" >}}
{{< tab "redact_text.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

def redact_text():
    # Open the document
    with Redactor("./sample.docx") as redactor:
        # Replace every occurrence of "John Doe" with "[personal]"
        redactor.apply(ExactPhraseRedaction("John Doe", ReplacementOptions("[personal]")))
        # Rasterize the result to a PDF named sample_redacted.pdf
        save_options = SaveOptions()
        save_options.add_suffix = True
        save_options.rasterize_to_pdf = True
        save_options.redacted_file_suffix = "redacted"
        redactor.save(save_options)

if __name__ == "__main__":
    redact_text()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/product-overview/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.pdf" >}}  
```text
Binary file (PDF, 1.0 MB)
```
[Download full output](/redaction/python-net/_output_files/product-overview/redact_text/sample_redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

For finer control, apply several redactions and keep the original format with `SaveOptions(rasterize_to_pdf=False)`:

{{< tabs "product-overview-redact-options" >}}
{{< tab "redact_with_options.py" >}}
```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, RegexRedaction, ReplacementOptions
from groupdocs.redaction.options import SaveOptions

def redact_with_options():
    with Redactor("./sample.docx") as redactor:
        # Redact a name and any 2+ digit number sequences
        redactor.apply(ExactPhraseRedaction("John Doe", ReplacementOptions("[personal]")))
        redactor.apply(RegexRedaction(r"\d{2,}", ReplacementOptions("[number]")))

        # Keep the original DOCX format instead of rasterizing to PDF
        options = SaveOptions()
        options.add_suffix = True
        options.rasterize_to_pdf = False
        options.redacted_file_suffix = "redacted"
        redactor.save(options)

if __name__ == "__main__":
    redact_with_options()
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/product-overview/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_redacted.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/redaction/python-net/_output_files/product-overview/redact_with_options/sample_redacted.docx)
{{< /tab >}}
{{< /tabs >}}

## Where to next

1. **Install the package** — [Installation]({{< ref "redaction/python-net/getting-started/installation.md" >}}) walks through PyPI and offline wheel installation for Windows, Linux, and macOS.
2. **Run your first redaction** — [Hello, World!]({{< ref "redaction/python-net/getting-started/hello-world.md" >}}) redacts a document in under five minutes.
3. **Explore runnable examples** — [How to Run Examples]({{< ref "redaction/python-net/getting-started/how-to-run-examples.md" >}}) clones the GitHub repository and runs every documented scenario locally or in Docker.
4. **Use it in depth** — the [Developer Guide]({{< ref "redaction/python-net/developer-guide/_index.md" >}}) covers every API surface with runnable, copy-paste code examples.
5. **Plug it into AI pipelines** — [AI Agents & LLM Integration]({{< ref "redaction/python-net/agents-and-llm-integration.md" >}}) explains the bundled `AGENTS.md`, the MCP server, and machine-readable docs.
