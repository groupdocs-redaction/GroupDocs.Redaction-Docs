---
id: agents-and-llm-integration
url: redaction/python-net/agents-and-llm-integration
title: AI agents and LLM integration
linkTitle: Agents and LLMs
weight: 6
description: "Use GroupDocs.Redaction for Python via .NET with AI coding assistants and LLMs — the bundled AGENTS.md reference, the GroupDocs MCP server, and machine-readable documentation."
keywords: AI agents, LLM, AGENTS.md, MCP, Claude, Cursor, Copilot, redaction, python
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Redaction for Python via .NET is designed to work smoothly with AI coding assistants such as Claude Code, Cursor, and GitHub Copilot in agent mode.

## Built into the package

The `groupdocs-redaction-net` wheel ships a bundled `AGENTS.md` reference. Once the package is installed, AI tools discover it automatically at `groupdocs/redaction/AGENTS.md`. It covers the canonical imports, the load → apply → save workflow, per-operation recipes, licensing, the full API-surface tables, and troubleshooting — everything an agent needs to write correct redaction code without guessing.

## MCP server

For on-demand documentation lookups, point your AI tool at the GroupDocs MCP server:

```json
{
  "mcpServers": {
    "groupdocs-docs": {
      "url": "https://docs.groupdocs.com/mcp"
    }
  }
}
```

This works with Claude Code (`~/.claude/settings.json`), Cursor (`.cursor/mcp.json`), VS Code Copilot (`.vscode/mcp.json`), and any MCP-compatible client.

## Machine-readable documentation

LLM-optimized documentation for retrieval-augmented generation and context loading is available at [`https://docs.groupdocs.com/redaction/python-net/llms-full.txt`](https://docs.groupdocs.com/redaction/python-net/llms-full.txt).

## AGENTS.md reference

The complete reference bundled inside the wheel is reproduced below.

````markdown
# GroupDocs.Redaction for Python via .NET -- AGENTS.md

> Instructions for AI agents working with this package.

Permanently remove sensitive content from documents -- redact text by exact phrase or regex, scrub or rewrite metadata, replace or delete annotations, black out image regions, remove pages, and rasterize the result so nothing redacted can be recovered. Works across Word, Excel, PowerPoint, PDF, images, and text formats through one unified API, with no MS Office or external software installed.

## Install

```bash
pip install groupdocs-redaction-net
```

**Python**: 3.5 - 3.14 | **Platforms**: Windows x64, Linux x64 (glibc 2.27+), macOS 12+ (x64, ARM64)

pip also installs `groupdocs-shared-net`, which holds the modules every GroupDocs Python package shares. For an offline install, download both wheels and install them together: `pip install --no-index --find-links <folder> groupdocs-redaction-net`.

## Resources

| Resource | URL |
|---|---|
| Documentation | https://docs.groupdocs.com/redaction/python-net/ |
| LLM-optimized docs | https://docs.groupdocs.com/redaction/python-net/llms-full.txt |
| API reference | https://reference.groupdocs.com/redaction/python-net/ |
| Code examples | https://docs.groupdocs.com/redaction/python-net/developer-guide/ |
| Release notes | https://releases.groupdocs.com/redaction/python-net/release-notes/ |
| PyPI | https://pypi.org/project/groupdocs-redaction-net/ |
| Free support forum | https://forum.groupdocs.com/c/redaction/ |
| Temporary license | https://purchase.groupdocs.com/temporary-license |

## MCP Server

If your environment has MCP configured, you can connect your AI tool to the GroupDocs documentation server for on-demand API lookups:

```json
{
  "mcpServers": {
    "groupdocs-docs": {
      "url": "https://docs.groupdocs.com/mcp"
    }
  }
}
```

Works with Claude Code (`~/.claude/settings.json`), Cursor (`.cursor/mcp.json`), VS Code Copilot (`.vscode/mcp.json`), and any MCP-compatible client. If MCP is unavailable, fall back to the LLM-optimized docs URL above and this file -- both are shipped inside the wheel.

To let an agent redact documents itself, without writing code, use the GroupDocs.Redaction MCP server: `docker run --rm -i -v $(pwd)/documents:/data ghcr.io/groupdocs-redaction/redaction-net-mcp:latest`, or `dnx GroupDocs.Redaction.Mcp --yes` with the .NET 10 SDK (https://docs.groupdocs.com/redaction/mcp/).

## Imports

```python
from groupdocs.redaction import (
    License, Metered, Redactor, RedactionPolicy,
    RedactionResult, RedactionStatus, RedactorChangeLog, RedactorLogEntry,
    FileType, IDocumentInfo,
    GroupDocsRedactionException, LicenseError,
)
from groupdocs.redaction.redactions import (
    # Text
    ExactPhraseRedaction, RegexRedaction, CellColumnRedaction, CellFilter,
    PageAreaRedaction, ReplacementOptions, RegionReplacementOptions,
    PageAreaFilter, PageRangeFilter,
    # Metadata
    EraseMetadataRedaction, MetadataSearchRedaction, MetadataFilters,
    # Annotations
    AnnotationRedaction, DeleteAnnotationRedaction,
    # Image / page
    ImageAreaRedaction, RemovePageRedaction, PageSeekOrigin,
    # Callback
    RedactionDescription, RedactionType, RedactionActionType,
)
from groupdocs.redaction.options import (
    LoadOptions, SaveOptions, RasterizationOptions, AdvancedRasterizationOptions,
    PdfComplianceLevel, PreviewOptions, PreviewFormats, RedactorSettings,
    WordprocessingSaveOptions, WordProcessingComplianceLevel,
)
from groupdocs.redaction.options.drawing import Color, Point, Size, Rectangle, Font, FontStyle
from groupdocs.redaction.integration.ocr import RecognizedImage, TextLine, TextFragment
from groupdocs.redaction.exceptions import (
    DocumentFormatException, IncorrectPasswordException, PasswordRequiredException,
    TrialLimitationsException,
)
```

Colors and geometry come from `groupdocs.redaction.options.drawing`. `groupdocs.pydrawing` types are not accepted (see "Upgrading from 26.6" below).

## Load + Apply + Save (the core workflow)

`Redactor` is the entry point. The flow is always: **open -> one or more `apply(...)` calls -> `save()`**. Each redaction mutates the in-memory document, so you can apply several before a single save. Use `Redactor` as a context manager so the native document handle is released.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("confidential", ReplacementOptions("[REDACTED]")))
    redactor.save()
```

**Redactor constructor.** `Redactor(file_path)` or `Redactor(stream)`, optionally with `load_options` and then `RedactorSettings`: `Redactor(file_path, LoadOptions(password="..."))`, `Redactor(stream, LoadOptions(...), RedactorSettings(...))`. `LoadOptions(FileType.DOCX)` names the format of a stream or of a file whose extension is not its format.

**`apply(...)`** accepts a single `Redaction`, a list of redactions, or a `RedactionPolicy`. It returns a `RedactorChangeLog` whose `.status` is a `RedactionStatus` (`APPLIED`, `PARTIALLY_APPLIED`, `SKIPPED`, `FAILED`); `.redaction_log` holds one entry per redaction, each with `.result.status` and `.result.error_message`.

**`save(...)`** writes the current state and returns the output path (when saving to a file). **By default it rasterizes the document to a PDF and appends a `_Redacted` suffix.** To control this, pass `SaveOptions` or `RasterizationOptions` (see Rasterization below).

## Operations

### Text redaction (exact phrase / regex)

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, RegexRedaction, ReplacementOptions
from groupdocs.redaction.options.drawing import Color

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[CUSTOMER]")))   # case-insensitive
    redactor.apply(ExactPhraseRedaction("ACME", True, ReplacementOptions("[CO]")))       # case-sensitive
    redactor.apply(RegexRedaction(r"\d{2,}", ReplacementOptions("[NUM]")))               # regex match
    redactor.apply(RegexRedaction(r"\bsecret\b", ReplacementOptions(Color.black)))       # draw a black box
    redactor.save()
```

`ReplacementOptions(text)` replaces the match with a string; `ReplacementOptions(Color)` draws a filled box over it. `ExactPhraseRedaction` also exposes `is_right_to_left`. `CellColumnRedaction(CellFilter, regex, ReplacementOptions)` targets a spreadsheet column.

### Metadata redaction

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import EraseMetadataRedaction, MetadataSearchRedaction, MetadataFilters

with Redactor("document.docx") as redactor:
    redactor.apply(EraseMetadataRedaction(MetadataFilters.ALL))             # erase everything
    redactor.apply(EraseMetadataRedaction(MetadataFilters.AUTHOR))          # erase one field
    redactor.apply(MetadataSearchRedaction(".*@acme\\.com", "[EMAIL]"))     # rewrite by value pattern
    redactor.save()
```

`MetadataFilters` is a flags-style enum: `AUTHOR`, `CATEGORY`, `COMMENTS`, `COMPANY`, `CONTENT_STATUS`, `CREATED_TIME`, `HYPERLINK_BASE`, `LAST_PRINTED`, `LAST_SAVED_BY`, `LAST_SAVED_TIME`, `NAME_OF_APPLICATION`, `MANAGER`, `REVISION_NUMBER`, `SUBJECT`, `TEMPLATE`, `TITLE`, `TOTAL_EDITING_TIME`, `VERSION`, `DESCRIPTION`, `KEYWORDS`, `CONTENT_TYPE`, `NONE` and `ALL`. `MetadataSearchRedaction(value_pattern, replacement, key_pattern=...)` can match on key and/or value.

**Check what metadata is left** (engine 26.10, measured in the saved files). `APPLIED` does not mean every property is gone.
- **Office and RTF:** Office Open XML (Word, Excel, PowerPoint), OpenDocument and RTF files lose the properties the filter names.
- **PDF saved as PDF:** the engine finds a PDF's properties through its XMP packet, so what only the document information dictionary holds stays. A PDF whose author is written only there keeps it, with nothing offered to the callback. A rasterized PDF (the default of `save()`) carries none of the original's author, title or subject.
- **Images:** JPEG files have their EXIF values blanked. PNG files lose their text chunks but keep their EXIF data. WEBP, TIFF and GIF files keep their metadata although the redaction reports `APPLIED`.

### Annotation redaction

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import AnnotationRedaction, DeleteAnnotationRedaction

with Redactor("document.pdf") as redactor:
    redactor.apply(AnnotationRedaction("(?i)approved", "[REVIEW]"))   # rewrite annotation text
    redactor.apply(DeleteAnnotationRedaction("(?i)internal"))         # delete matching annotations
    redactor.save()
```

### Image-area and page-area redaction

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ImageAreaRedaction, PageAreaRedaction, RegionReplacementOptions, ReplacementOptions
from groupdocs.redaction.options.drawing import Point, Size, Color

with Redactor("scan.pdf") as redactor:
    # black out a fixed rectangle on every page
    redactor.apply(ImageAreaRedaction(Point(50, 60), RegionReplacementOptions(Color.black, Size(200, 80))))
    # redact text AND its image rendering in a page area
    redactor.apply(PageAreaRedaction(r"\d{3}-\d{2}-\d{4}", ReplacementOptions("[SSN]"),
                                     RegionReplacementOptions(Color.black, Size(120, 20))))
    redactor.save()
```

Scope a redaction to pages or a page area with `ReplacementOptions.filters = [PageRangeFilter(PageSeekOrigin.END, 0, 1), PageAreaFilter(Point(x, y), Size(w, h))]` (PDF documents).

### Page removal

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import RemovePageRedaction, PageSeekOrigin

with Redactor("document.pdf") as redactor:
    redactor.apply(RemovePageRedaction(PageSeekOrigin.BEGIN, 0, 1))   # drop the first page
    redactor.save()
```

Documents and multi-page TIFF files lose the pages asked for. Multi-frame images on engine 26.10:
- **Animated GIF:** loses fewer frames than asked, and still reports `APPLIED`: removing the first or the last of 8 frames leaves 8.
- **Animated WEBP:** removing the first frame raises "Index was out of range".

Count the frames of the output.

### Redaction callback (approve or reject each change)

`RedactorSettings` is the **third** Redactor argument, after `load_options`, so pass `LoadOptions()` (or a configured one) as well. A function, or an object with `accept_redaction(description)`, is called for each change and returns `True` to make it or `False` to skip it.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.redaction.options import LoadOptions, RedactorSettings

def accept(description):
    # description.original_text, .redaction_type, .action_type, .replacement
    return "keep-me" not in (description.original_text or "")   # return False to skip this match

with Redactor("document.docx", LoadOptions(), RedactorSettings(callback=accept)) as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))
    redactor.save()
```

`description` is the engine's `RedactionDescription`, valid during the call: `redaction_type` (`RedactionType`), `action_type` (`RedactionActionType`), `original_text`, `replacement` (`.original_text`, `.replacement`), `image_area_replacement`, and a writable `details`. An exception in the callback does not propagate: the redaction's log entry becomes `FAILED` with the message.

### Logger

An object with `error(message)`, `warning(message)` and `trace(message)` (any of them), or a function `fn(level, message)`, receives what the engine reports. A logger that raises is printed to stderr and never stops the redaction.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import LoadOptions, RedactorSettings
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

class Log(object):
    def __init__(self):
        self.errors, self.traces = [], []
    def error(self, message): self.errors.append(message)
    def warning(self, message): pass
    def trace(self, message): self.traces.append(message)

log = Log()
with Redactor("document.docx", LoadOptions(), RedactorSettings(logger=log)) as redactor:
    redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions("[X]")))
    if not log.errors:
        redactor.save()
print(log.traces)
```

`RedactorSettings` takes one argument by kind (`RedactorSettings(log)`, `RedactorSettings(accept)`, `RedactorSettings(connector)`), keywords (`logger=`, `callback=`, `ocr_connector=`), or all three in that order.

### OCR connector (text in images)

GroupDocs.Redaction ships no OCR engine. An object with `recognize(image_stream)`, or a function, returns what an OCR engine found as a `RecognizedImage` of `TextLine`s of `TextFragment(text, Rectangle(x, y, width, height))`, or `None`. `image_stream.read()` gives the image bytes. Report each recognized line as one `TextFragment`, with the line's text and bounding rectangle: the engine boxes a match inside a fragment by character position, but a match that spans two fragments is reported `APPLIED` and not painted (engine 26.10). Near the end of a long line the estimated box can fall a few pixels short, so check the output.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.integration.ocr import RecognizedImage, TextFragment, TextLine
from groupdocs.redaction.options import LoadOptions, RedactorSettings
from groupdocs.redaction.options.drawing import Color, Rectangle
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

class Connector(object):
    def recognize(self, image_stream):
        data = image_stream.read()   # hand these bytes to an OCR engine, e.g. pytesseract
        # one fragment per recognized line: its text and its bounding rectangle
        return RecognizedImage([TextLine([TextFragment("Emily Johnson", Rectangle(40, 40, 230, 40))])])

with Redactor("scan.png", LoadOptions(), RedactorSettings(ocr_connector=Connector())) as redactor:
    print(redactor.apply(ExactPhraseRedaction("Emily Johnson", ReplacementOptions(Color.black))).status.name)
```

### Rasterization (flatten to PDF)

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.redaction.options import SaveOptions, AdvancedRasterizationOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))

    # (a) default: rasterize to PDF, "_Redacted" suffix
    redactor.save()

    # (b) keep original format, with a suffix
    redactor.save(SaveOptions(rasterize_to_pdf=False, add_suffix=True))

    # (c) rasterize with anti-extraction effects
    so = SaveOptions()
    so.add_suffix = True
    so.redacted_file_suffix = "scan"
    so.rasterization.enabled = True
    so.rasterization.add_advanced_option(AdvancedRasterizationOptions.NOISE)
    so.rasterization.add_advanced_option(AdvancedRasterizationOptions.GRAYSCALE)
    redactor.save(so)
```

`save_options.rasterization` is a `RasterizationOptions`: `enabled`, `page_index`, `page_count`, `compliance` (`PdfComplianceLevel.AUTO` / `PDF_A1A`), `add_advanced_option(AdvancedRasterizationOptions.{TILT,NOISE,BORDER,GRAYSCALE})`. A new `SaveOptions()` keeps the format and adds no suffix, so `save(SaveOptions())` overwrites the source file; `save()` with no argument rasterizes and adds `_Redacted`. For a Word document saved in its own format, `save_options.wordprocessing_save_options.ooxml_compliance = WordProcessingComplianceLevel.STRICT` (or `ECMA`, `TRANSITIONAL`) sets its OOXML compliance level; unset, the original's is kept.

### Save to a stream

`save(stream, save_options)` or `save(stream, rasterization_options)` writes to any writable stream: an open binary file or an `io.BytesIO`, which holds the document after the call. A PDF/A save (`rasterization_options.compliance = PdfComplianceLevel.PDF_A1A`) reads its output back, so open a file with `"w+b"`: with `"wb"` the call raises `NotImplementedError: Stream does not support reading`.

```python
import io
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import SaveOptions
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))
    buf = io.BytesIO()
    redactor.save(buf, SaveOptions(rasterize_to_pdf=False))     # keep original format
    data = buf.getvalue()
```

### Redaction policy (reusable rule set)

```python
from groupdocs.redaction import Redactor, RedactionPolicy
from groupdocs.redaction.redactions import ExactPhraseRedaction, RegexRedaction, ReplacementOptions

policy = RedactionPolicy([
    ExactPhraseRedaction("ACME", ReplacementOptions("[CO]")),
    RegexRedaction(r"\d{2,}", ReplacementOptions("[NUM]")),
])

with Redactor("document.docx") as redactor:
    redactor.apply(policy=policy)
    redactor.save()
```

Build the policy in memory and reuse it across documents. A policy can also be saved to and loaded from an XML file: `policy.save(path)`, `RedactionPolicy.load(path)`. Engine 26.10 saves a case-insensitive `ExactPhraseRedaction` (the default) without a `caseSensitive` attribute, and `load` rejects that file with `String '' was not recognized as a valid Boolean`: add `caseSensitive="false"` to those `<exactPhraseRedaction>` elements before loading it.

### Document info & preview

```python
import io
from groupdocs.redaction import Redactor
from groupdocs.redaction.options import PreviewOptions, PreviewFormats

with Redactor("document.pdf") as redactor:
    info = redactor.get_document_info()
    print(info.file_type.file_format, info.page_count, info.size)

    pages = {}
    def create_page_stream(page_number):
        pages[page_number] = io.BytesIO()
        return pages[page_number]

    options = PreviewOptions(create_page_stream)
    options.width, options.height = 300, 400       # both required
    options.page_numbers = [1]                    # required
    options.preview_format = PreviewFormats.PNG
    redactor.generate_preview(options)
    print(len(pages[1].getvalue()))
```

`get_document_info()` returns an `IDocumentInfo`: `file_type` (a `FileType`), `page_count`, `size`, `pages`. `generate_preview(PreviewOptions(create_page_stream[, release_page_stream]))` renders pages to images (`PreviewFormats.PNG`/`JPEG`/`BMP`). `create_page_stream(page_number)` returns an open binary file or an `io.BytesIO`; `release_page_stream(page_number, stream)` gets that stream back once the page is written. Set `width`, `height` and `page_numbers`: the engine raises an error when any is left unset. A preview shows the document as loaded, before the redactions applied since.

## Licensing

```python
from groupdocs.redaction import License

# From file
License().set_license("path/to/license.lic")

# From stream
with open("license.lic", "rb") as f:
    License().set_license(f)

print(License().is_licensed)
```

Or auto-apply: `export GROUPDOCS_LIC_PATH="path/to/license.lic"` (a file or a URL). A licence from `GROUPDOCS_LIC_PATH` that cannot be applied raises `LicenseError` from the first engine call; `GROUPDOCS_LIC_STRICT=0` makes it a `LicenseWarning` and evaluation mode instead.

Metered licensing is also available:

```python
from groupdocs.redaction import Metered

public_key, private_key = "*****", "*****"   # your metered keys
if "*" not in public_key + private_key:      # placeholder keys are rejected
    Metered().set_metered_key(public_key, private_key)
    print(Metered.get_consumption_quantity(), Metered.get_consumption_credit())
```

**Evaluation vs licensed.** Without a license the library still runs: **up to 25 documents may be opened per process** (the next open raises `TrialLimitationsException`), saved documents carry trial badges, and **long documents are cut short**. A rasterized PDF keeps its first 4 pages, a long Word document saved in its own format loses part of its text (152 of 276 paragraphs in a 10-page sample), and on a PDF of more than 4 pages `get_document_info()` raises `At most 4 elements (for any collection) can be viewed in evaluation mode` while page and metadata redactions report `FAILED` or `SKIPPED`. Do not judge output completeness unlicensed. Set `GROUPDOCS_LIC_PATH` (or call `License().set_license(...)`) and re-run to clear these. A 30-day full license is free: https://purchase.groupdocs.com/temporary-license

## API Reference

### Redactor

| Method | Returns | Description |
|---|---|---|
| `Redactor(file_path / stream [, load_options [, settings]])` | | Open by path or binary stream; optional `LoadOptions` and `RedactorSettings`. Use as a context manager. |
| `apply(redaction)` / `apply([...])` / `apply(policy=...)` | `RedactorChangeLog` | Apply one redaction, a list, or a `RedactionPolicy`. `.status` is a `RedactionStatus`. |
| `save([save_options])` | `str` | Write to disk; default rasterizes to PDF + `_Redacted` suffix. Returns the output path. |
| `save(stream, save_options / rasterization_options)` | `None` | Write to a stream (an open binary file or `io.BytesIO`). |
| `generate_preview(preview_options)` | `None` | Render pages to images via a `create_page_stream` callback. |
| `get_document_info()` | `IDocumentInfo` | `file_type`, `page_count`, `size`, `pages`. |
| `dispose()` | `None` | Release native resources (handled by `with`). |

### Redactions

| Type | Notes |
|---|---|
| `ExactPhraseRedaction(phrase [, is_case_sensitive], options)` | Replace/box an exact phrase. `is_right_to_left` for RTL. |
| `RegexRedaction(pattern, options)` | Replace/box a regex match. |
| `CellColumnRedaction(CellFilter, regex, options)` | Redact a spreadsheet column. |
| `PageAreaRedaction(regex, options, RegionReplacementOptions)` | Text + image redaction over a page area. |
| `EraseMetadataRedaction(MetadataFilters)` | Erase metadata by filter. |
| `MetadataSearchRedaction(value_pattern, replacement [, key_pattern])` | Rewrite metadata by key/value pattern. |
| `AnnotationRedaction(pattern, replacement)` / `DeleteAnnotationRedaction([pattern])` | Rewrite or delete annotations. |
| `ImageAreaRedaction(Point, RegionReplacementOptions)` | Black out a rectangle on a page. |
| `RemovePageRedaction(PageSeekOrigin, index, count)` | Remove pages from the start/end. |
| `ReplacementOptions(text)` / `ReplacementOptions(Color)` | Text replacement vs. a filled box. `filters` (`PageRangeFilter`, `PageAreaFilter`). |
| `RegionReplacementOptions(fill_color, size)` / `(fill_color, font, expected_text)` | Box geometry for image/page-area redactions. |

### Options & enums

| Type | Notes |
|---|---|
| `LoadOptions([password] / [file_type])` | `password`, `pre_rasterize`, `file_type`. |
| `SaveOptions(rasterize_to_pdf=..., add_suffix=..., redacted_file_suffix=...)` | Control format + suffix; `wordprocessing_save_options.ooxml_compliance`. |
| `RasterizationOptions()` | `enabled`, `page_index`, `page_count`, `compliance`, `add_advanced_option(...)`. |
| `AdvancedRasterizationOptions` | `NONE`, `TILT`, `NOISE`, `BORDER`, `GRAYSCALE`. |
| `PdfComplianceLevel` | `AUTO`, `PDF_A1A`. |
| `WordProcessingComplianceLevel` | `ECMA`, `TRANSITIONAL`, `STRICT`. |
| `PreviewOptions(create_page_stream [, release_page_stream])` | `width`, `height`, `page_numbers` (all required), `preview_format`. |
| `PreviewFormats` | `PNG`, `JPEG`, `BMP`. |
| `RedactorSettings(logger=..., callback=..., ocr_connector=...)` | A logger, a redaction callback, an OCR connector (Python objects or functions). |
| `MetadataFilters` | `AUTHOR`, `COMPANY`, `COMMENTS`, `MANAGER`, `TITLE`, `SUBJECT`, `KEYWORDS`, ..., `ALL`. |
| `RedactionStatus` | `APPLIED`, `PARTIALLY_APPLIED`, `SKIPPED`, `FAILED`. |
| `RedactionType` / `RedactionActionType` | `TEXT`/`METADATA`/`ANNOTATION`/`IMAGE_AREA`/`PAGE`; `REPLACEMENT`/`CLEANUP`/`DELETION`. |
| `PageSeekOrigin` | `BEGIN`, `END`. |
| `Color`, `Point`, `Size`, `Rectangle`, `Font`, `FontStyle` | `groupdocs.redaction.options.drawing`: `Color.black` (named colors), `Color.from_argb(a, r, g, b)`, `Color.from_name("Red")`, `Point(x, y)`, `Size(w, h)`, `Rectangle(x, y, w, h)`. |

### License / Metered

`License().set_license(path_or_stream)` · `License().is_licensed` · `Metered().set_metered_key(public, private)` · `Metered.get_consumption_quantity()` · `Metered.get_consumption_credit()`

## Key Patterns

- **Properties**: use `snake_case` -- auto-mapped to .NET `PascalCase`; a misspelled property name raises `AttributeError` instead of being ignored
- **Context managers**: `with Redactor(...) as r:` ensures the document handle is released
- **Chaining**: each `apply()` mutates in place; run several before one `save()`
- **Default save rasterizes**: `save()` produces a PDF + `_Redacted` suffix; `SaveOptions(rasterize_to_pdf=False, add_suffix=True)` keeps the source format. A bare `SaveOptions()` adds no suffix and overwrites the source
- **Colors / geometry**: `Color`, `Point`, `Size`, `Rectangle` come from `groupdocs.redaction.options.drawing`; `ReplacementOptions(Color)` draws a box
- **Regex args**: pass a plain Python regex string -- the binding wraps it as a .NET `Regex`
- **Streams**: pass `open("file", "rb")` or `io.BytesIO(data)` where .NET expects a Stream; an empty `BytesIO` passed to `save(stream, ...)` holds the output afterwards
- **Enums**: `MetadataFilters.ALL`, `PreviewFormats.PNG`, `RedactionStatus.APPLIED`
- **Callbacks**: a Python function or object stands in for the redaction callback, the logger and the OCR connector; preview streams take functions
- **Exceptions**: catch `PasswordRequiredException` / `IncorrectPasswordException` / `DocumentFormatException` / `TrialLimitationsException` (all subclass `GroupDocsRedactionException`, which the package root exports)

## Platform Requirements

| Platform | Requirements |
|---|---|
| Windows | None |
| Linux | ICU (`libicu`), `fontconfig` and fonts: `apt install libicu-dev fontconfig ttf-mscorefonts-installer` |
| macOS | None |

`libgdiplus` is not needed on any platform.

## Troubleshooting

**`Trial mode allows opening up to 25 documents per process` / `TrialLimitationsException`** -- no license. Apply one with `License().set_license(...)` or set `GROUPDOCS_LIC_PATH`; a free 30-day license is at https://purchase.groupdocs.com/temporary-license

**`At most 4 elements (for any collection) can be viewed in evaluation mode`** -- no license, and a PDF of more than 4 pages. Apply a license; evaluation mode also cuts long documents short (see "Evaluation vs licensed").

**`LicenseError` on the first call** -- the licence named by `GROUPDOCS_LIC_PATH` cannot be applied; the message names the file or URL and the engine's reason.

**`PasswordRequiredException` / `IncorrectPasswordException`** -- the source is encrypted. Open it with `Redactor(path, LoadOptions(password="..."))`.

**`DocumentFormatException`** -- the file format isn't supported or the file is corrupted. Check it against the supported-formats list.

**`String '' was not recognized as a valid Boolean` from `RedactionPolicy.load`** -- the file was written by `policy.save()` with a case-insensitive `ExactPhraseRedaction`. Add `caseSensitive="false"` to its `<exactPhraseRedaction>` elements.

**`NotImplementedError: Stream does not support reading` from `save(stream, ...)`** -- a PDF/A save reads its output back. Open the file with `"w+b"`, or save to an `io.BytesIO`.

**`TypeError: ... no overload matched` with a `Color`, `Point` or `Size`** -- the value comes from `groupdocs.pydrawing`. Import them from `groupdocs.redaction.options.drawing`.

**Process exits with code 134, `Couldn't find a valid ICU package`** (Linux) -- install ICU: `sudo apt install libicu-dev`. Do NOT set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT`.

**`DllNotFoundException` opening a presentation** (Linux; PPTX, PPT, ODP, ...) -- the presentation engine links fontconfig: `sudo apt install libfontconfig1`.

**Garbled text / missing fonts** -- install fonts: `sudo apt install ttf-mscorefonts-installer fontconfig && sudo fc-cache -f`

**An `Aspose/Drawing/SystemFontCache.xml` appears in the working directory** (Linux) -- the engine's font cache. The package creates `~/.local/share` (or `$XDG_DATA_HOME`) before the engine starts, and the cache is kept there; it lands in the working directory only when that folder cannot be created, as in a read-only home. Set `XDG_DATA_HOME` to a writable folder.

**`DllNotFoundException: libSkiaSharp`** -- stale system copy conflicts with bundled version. Rename it: `sudo mv /usr/local/lib/libSkiaSharp.dylib /usr/local/lib/libSkiaSharp.dylib.bak`

**`TypeLoadException`** -- reinstall: `pip install --force-reinstall groupdocs-redaction-net`

**Still stuck?** Post your question at https://forum.groupdocs.com/c/redaction/ -- the development team responds directly.

## Upgrading from 26.6

| 26.6 | 26.11 |
|---|---|
| `from groupdocs.pydrawing import Color, Point, Size` | `from groupdocs.redaction.options.drawing import Color, Point, Size` (also `Rectangle`, `Font`, `FontStyle`) |
| `from groupdocs.redaction import Color` | `from groupdocs.redaction.options.drawing import Color` |
| redaction callback: `description.redaction_type` / `.action_type` were names (`"Text"`) | enums: `RedactionType.TEXT`, `RedactionActionType.REPLACEMENT` (`.name` gives the name) |
| a logger, an OCR connector or a preview callable raised `TypeError` | each takes a Python object or function |
| evaluation: 1 document, 1 redaction, 4 replacements | evaluation: 25 documents per process; long documents still cut short |
| Linux/macOS: rasterized PDF output and image-area redaction raised `PlatformNotSupportedException` | work on every platform, with no `libgdiplus` |
````
