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

**Python**: 3.5 - 3.14 | **Platforms**: Windows, Linux, macOS

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

## Imports

```python
from groupdocs.redaction import (
    License, Metered, Redactor, RedactionPolicy,
    RedactionResult, RedactionStatus, RedactorChangeLog, RedactorLogEntry,
    FileType, IDocumentInfo,
)
from groupdocs.redaction.redactions import (
    # Text
    ExactPhraseRedaction, RegexRedaction, CellColumnRedaction, CellFilter,
    PageAreaRedaction, ReplacementOptions, RegionReplacementOptions,
    # Metadata
    EraseMetadataRedaction, MetadataSearchRedaction, MetadataFilters,
    # Annotations
    AnnotationRedaction, DeleteAnnotationRedaction,
    # Image / page
    ImageAreaRedaction, RemovePageRedaction, PageSeekOrigin,
    # Custom rules / callback
    ICustomRedactionHandler, CustomRedactionContext, CustomRedactionResult,
    IRedactionCallback, RedactionDescription, RedactionType, RedactionActionType,
)
from groupdocs.redaction.options import (
    LoadOptions, SaveOptions, RasterizationOptions, AdvancedRasterizationOptions,
    PdfComplianceLevel, PreviewOptions, PreviewFormats, RedactorSettings,
)
from groupdocs.redaction.exceptions import (
    GroupDocsRedactionException, DocumentFormatException,
    IncorrectPasswordException, PasswordRequiredException, TrialLimitationsException,
)
from groupdocs.pydrawing import Color, Point, Size   # for box / image-area redactions
```

## Load + Apply + Save (the core workflow)

`Redactor` is the entry point. The flow is always: **open → one or more `apply(...)` calls → `save()`**. Each redaction mutates the in-memory document, so you can apply several before a single save. Use `Redactor` as a context manager so the native document handle is released.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("confidential", ReplacementOptions("[REDACTED]")))
    redactor.save()
```

**Redactor constructor.** `Redactor(file_path)` or `Redactor(stream)`, optionally with `load_options` and/or `RedactorSettings`: `Redactor(file_path, LoadOptions(password="..."))`, `Redactor(stream, LoadOptions(...), RedactorSettings(...))`.

**`apply(...)`** accepts a single `Redaction`, a list of redactions, or a `RedactionPolicy`. It returns a `RedactorChangeLog` whose `.status` is a `RedactionStatus` (`APPLIED`, `PARTIALLY_APPLIED`, `SKIPPED`, `FAILED`).

**`save(...)`** writes the current state and returns the output path (when saving to a file). **By default it rasterizes the document to a PDF and appends a `_Redacted` suffix.** To control this, pass `SaveOptions` or `RasterizationOptions` (see Rasterization below).

## Operations

### Text redaction (exact phrase / regex)

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, RegexRedaction, ReplacementOptions
from groupdocs.pydrawing import Color

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("John Doe", ReplacementOptions("[CUSTOMER]")))   # case-insensitive
    redactor.apply(ExactPhraseRedaction("ACME", True, ReplacementOptions("[CO]")))       # case-sensitive
    redactor.apply(RegexRedaction(r"\d{2,}", ReplacementOptions("[NUM]")))               # regex match
    redactor.apply(RegexRedaction(r"\bsecret\b", ReplacementOptions(Color.BLACK)))       # draw a black box
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

`MetadataFilters` is a flags-style enum: `AUTHOR`, `COMPANY`, `COMMENTS`, `MANAGER`, `TITLE`, `SUBJECT`, `KEYWORDS`, `CONTENT_STATUS`, … and `ALL`. `MetadataSearchRedaction(value_pattern, replacement, key_pattern=...)` can match on key and/or value.

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
from groupdocs.pydrawing import Point, Size, Color

with Redactor("scan.pdf") as redactor:
    # black out a fixed rectangle on every page
    redactor.apply(ImageAreaRedaction(Point(50, 60), RegionReplacementOptions(Color.BLACK, Size(200, 80))))
    # redact text AND its image rendering in a page area
    redactor.apply(PageAreaRedaction(r"\d{3}-\d{2}-\d{4}", ReplacementOptions("[SSN]"),
                                     RegionReplacementOptions(Color.BLACK, Size(120, 20))))
    redactor.save()
```

### Page removal

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import RemovePageRedaction, PageSeekOrigin

with Redactor("document.pdf") as redactor:
    redactor.apply(RemovePageRedaction(PageSeekOrigin.BEGIN, 0, 1))   # drop the first page
    redactor.save()
```

### Custom redaction rule / callback

A `RedactorSettings(callback=...)` receives every redaction description and decides whether to accept it. Pass a plain Python callable -- the binding wraps it as the .NET `IRedactionCallback` automatically. `RedactorSettings` is the **third** Redactor argument, after `load_options`, so pass `LoadOptions()` (or a configured one) as well.

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.redaction.options import LoadOptions, RedactorSettings

def accept(description):
    # description.original_text, .redaction_type, .action_type
    return "keep-me" not in (description.original_text or "")   # return False to skip this match

with Redactor("document.docx", LoadOptions(), RedactorSettings(callback=accept)) as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))
    redactor.save()
```

The callback returns `bool` (accept/reject) -- `IRedactionCallback.accept_redaction` returns a boolean. For text-rewriting rules use `ICustomRedactionHandler` via `ReplacementOptions.custom_redaction`.

### Rasterization (flatten to PDF)

```python
from groupdocs.redaction import Redactor
from groupdocs.redaction.redactions import ExactPhraseRedaction, ReplacementOptions
from groupdocs.redaction.options import SaveOptions, RasterizationOptions, AdvancedRasterizationOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))

    # (a) default: rasterize to PDF, "_Redacted" suffix
    redactor.save()

    # (b) keep original format, no rasterization
    redactor.save(SaveOptions(rasterize_to_pdf=False))

    # (c) rasterize with anti-extraction effects
    ro = RasterizationOptions()
    ro.enabled = True
    ro.add_advanced_option(AdvancedRasterizationOptions.NOISE)
    ro.add_advanced_option(AdvancedRasterizationOptions.GRAYSCALE)
    redactor.save(ro)
```

`RasterizationOptions`: `enabled`, `page_index`, `page_count`, `compliance` (`PdfComplianceLevel.AUTO` / `PDF_A1A`), `add_advanced_option(AdvancedRasterizationOptions.{TILT,NOISE,BORDER,GRAYSCALE})`.

### Save to a stream

`save(stream, rasterization_options)` writes to any writable stream. Return a path-backed or `io.BytesIO` stream; `BytesIO` is updated after the call.

```python
import io
from groupdocs.redaction.options import RasterizationOptions

with Redactor("document.docx") as redactor:
    redactor.apply(ExactPhraseRedaction("secret", ReplacementOptions("[X]")))
    ro = RasterizationOptions(); ro.enabled = False     # keep original format
    buf = io.BytesIO()
    redactor.save(buf, ro)
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

Build the policy in memory and reuse it across documents. (A policy can also be authored as an XML file and read with `RedactionPolicy.load(path)`.)

### Document info & preview

```python
with Redactor("document.pdf") as redactor:
    info = redactor.get_document_info()
    print(info.file_type.file_format, info.page_count, info.size)
```

`get_document_info()` returns an `IDocumentInfo`: `file_type` (a `FileType`), `page_count`, `size`, `pages`. `generate_preview(PreviewOptions(...))` renders pages to images (`PreviewFormats.PNG`/`JPEG`/`BMP`) via a `create_page_stream(page_number)` callback that returns a writable file/path stream (not `BytesIO`).

## Licensing

```python
from groupdocs.redaction import License

# From file
License().set_license("path/to/license.lic")

# From stream
with open("license.lic", "rb") as f:
    License().set_license(f)
```

Or auto-apply: `export GROUPDOCS_LIC_PATH="path/to/license.lic"`

Metered licensing is also available:

```python
from groupdocs.redaction import Metered

Metered().set_metered_key("public-key", "private-key")
print(Metered().get_consumption_quantity(), Metered().get_consumption_credit())
```

**Evaluation vs licensed.** Without a license the library still runs, but **only one document may be opened per process** (subsequent opens raise a trial-limitation error), PDF output carries an evaluation watermark, and other formats show an equivalent evaluation mark. Set `GROUPDOCS_LIC_PATH` (or call `License().set_license(...)`) and re-run to clear these. A 30-day full license is free: https://purchase.groupdocs.com/temporary-license

## API Reference

### Redactor

| Method | Returns | Description |
|---|---|---|
| `Redactor(file_path / stream [, load_options [, settings]])` | | Open by path or binary stream; optional `LoadOptions` and `RedactorSettings`. Use as a context manager. |
| `apply(redaction)` / `apply(redactions=[...])` / `apply(policy=...)` | `RedactorChangeLog` | Apply one redaction, a list, or a `RedactionPolicy`. `.status` is a `RedactionStatus`. |
| `save([save_options])` | `str` | Write to disk; default rasterizes to PDF + `_Redacted` suffix. Returns the output path. |
| `save(stream [, rasterization_options])` | `str` | Write to a stream (file/path stream or `io.BytesIO`). |
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
| `AnnotationRedaction(pattern, replacement)` / `DeleteAnnotationRedaction(pattern)` | Rewrite or delete annotations. |
| `ImageAreaRedaction(Point, RegionReplacementOptions)` | Black out a rectangle on a page. |
| `RemovePageRedaction(PageSeekOrigin, index, count)` | Remove pages from the start/end. |
| `ReplacementOptions(text)` / `ReplacementOptions(Color)` | Text replacement vs. a filled box. `filters`, `custom_redaction`. |
| `RegionReplacementOptions(fill_color, size [, font, expected_text])` | Box geometry for image/page-area redactions. |

### Options & enums

| Type | Notes |
|---|---|
| `LoadOptions(password=..., pre_rasterize=...)` | Open protected / pre-rasterized input. |
| `SaveOptions(rasterize_to_pdf=..., suffix=...)` | Control format + `_Redacted` suffix. |
| `RasterizationOptions()` | `enabled`, `page_index`, `page_count`, `compliance`, `add_advanced_option(...)`. |
| `AdvancedRasterizationOptions` | `NONE`, `TILT`, `NOISE`, `BORDER`, `GRAYSCALE`. |
| `PdfComplianceLevel` | `AUTO`, `PDF_A1A`. |
| `PreviewOptions(create_page_stream [, release_page_stream])` | `width`, `height`, `page_numbers`, `preview_format`. |
| `PreviewFormats` | `PNG`, `JPEG`, `BMP`. |
| `RedactorSettings(logger=..., callback=..., ocr_connector=...)` | Inject a logger, an `IRedactionCallback`, or OCR. |
| `MetadataFilters` | `AUTHOR`, `COMPANY`, `COMMENTS`, `MANAGER`, `TITLE`, `SUBJECT`, `KEYWORDS`, …, `ALL`. |
| `RedactionStatus` | `APPLIED`, `PARTIALLY_APPLIED`, `SKIPPED`, `FAILED`. |
| `RedactionType` / `RedactionActionType` | `TEXT`/`METADATA`/`ANNOTATION`/`IMAGE_AREA`/`PAGE`; `REPLACEMENT`/`CLEANUP`/`DELETION`. |
| `PageSeekOrigin` | `BEGIN`, `END`. |

### License / Metered

`License().set_license(path_or_stream)` · `Metered().set_metered_key(public, private)` · `Metered().get_consumption_quantity()` · `Metered().get_consumption_credit()`

## Key Patterns

- **Properties**: use `snake_case` -- auto-mapped to .NET `PascalCase`
- **Context managers**: `with Redactor(...) as r:` ensures the document handle is released
- **Chaining**: each `apply()` mutates in place; run several before one `save()`
- **Default save rasterizes**: `save()` produces a PDF + `_Redacted` suffix; pass `SaveOptions(rasterize_to_pdf=False)` to keep the source format
- **Colors / geometry**: `Color`, `Point`, `Size` come from `groupdocs.pydrawing`; `ReplacementOptions(Color)` draws a box
- **Regex args**: pass a plain Python regex string -- the binding wraps it as a .NET `Regex`
- **Streams**: pass `open("file", "rb")` or `io.BytesIO(data)` where .NET expects a Stream; `BytesIO` is updated after `save(stream)`
- **Enums**: case-insensitive, lazy-loaded (e.g., `MetadataFilters.ALL`, `PreviewFormats.PNG`)
- **Callbacks**: a Python callable is accepted for `IRedactionCallback`; it returns `bool` to accept/reject each match
- **Exceptions**: catch `PasswordRequiredException` / `IncorrectPasswordException` / `DocumentFormatException` / `TrialLimitationsException` (all subclass `GroupDocsRedactionException`)

## Platform Requirements

| Platform | Requirements |
|---|---|
| Windows | None |
| Linux | `apt install libgdiplus libfontconfig1 ttf-mscorefonts-installer` |
| macOS | `brew install mono-libgdiplus` |

## Troubleshooting

**`Trial mode allows only 1 document to open` / `TrialLimitationsException`** -- no license. Apply one with `License().set_license(...)` or set `GROUPDOCS_LIC_PATH`; a free 30-day license is at https://purchase.groupdocs.com/temporary-license

**`PasswordRequiredException` / `IncorrectPasswordException`** -- the source is encrypted. Open it with `Redactor(path, LoadOptions(password="..."))`.

**`DocumentFormatException`** -- the file format isn't supported or the file is corrupted. Check it against the supported-formats list.

**`System.Drawing.Common is not supported`** -- install libgdiplus: `sudo apt install libgdiplus` (Linux) / `brew install mono-libgdiplus` (macOS)

**`Gdip` type initializer exception** -- outdated libgdiplus: `brew reinstall mono-libgdiplus` (macOS)

**Garbled text / missing fonts** -- install fonts: `sudo apt install ttf-mscorefonts-installer fontconfig && sudo fc-cache -f`

**`DllNotFoundException: libSkiaSharp`** -- stale system copy conflicts with bundled version. Rename it: `sudo mv /usr/local/lib/libSkiaSharp.dylib /usr/local/lib/libSkiaSharp.dylib.bak`

**`DOTNET_SYSTEM_GLOBALIZATION_INVARIANT` errors** -- do NOT set this. Install ICU: `sudo apt install libicu-dev`

**`TypeLoadException`** -- reinstall: `pip install --force-reinstall groupdocs-redaction-net`

**Still stuck?** Post your question at https://forum.groupdocs.com/c/redaction/ -- the development team responds directly.
````
