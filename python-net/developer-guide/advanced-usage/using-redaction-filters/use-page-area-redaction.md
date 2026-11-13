---
id: use-page-area-redaction
url: redaction/python-net/use-page-area-redaction
title: Use PageAreaRedaction
weight: 3
description: "Redact text, images and annotations inside an area of chosen pages with PageAreaRedaction in GroupDocs.Redaction for Python via .NET."
keywords: PageAreaRedaction, page area, page range, PageAreaFilter, PageRangeFilter, PDF, python, GroupDocs.Redaction
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
---
[PageAreaRedaction](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/pagearearedaction/) redacts an area of chosen pages: the text that matches a regular expression, and the images and annotations, inside that area. Scope it with [redaction filters]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-redaction-filters/_index.md" >}}) on its text options: a [PageRangeFilter](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/pagerangefilter/) for the pages and a [PageAreaFilter](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction.redactions/pageareafilter/) for the area.

The following example redacts the right half of the last page of a PDF document:

{{< tabs "code-example-use-page-area-redaction" >}}
{{< tab "use_page_area_redaction.py" >}}
```python
from groupdocs.redaction import Redactor, RedactionStatus
from groupdocs.redaction.options.drawing import Color, Point, Size
from groupdocs.redaction.redactions import (
    PageAreaFilter,
    PageAreaRedaction,
    PageRangeFilter,
    PageSeekOrigin,
    RegionReplacementOptions,
    ReplacementOptions,
)


def use_page_area_redaction():
    with Redactor("./multipage_sample.pdf") as redactor:
        # Text in the area: replaced
        text_options = ReplacementOptions("[redacted]")
        text_options.filters = [
            PageRangeFilter(PageSeekOrigin.END, 0, 1),           # the last page
            PageAreaFilter(Point(306, 0), Size(306, 792)),       # its right half
        ]
        # Images in the area: covered with a box
        image_options = RegionReplacementOptions(Color.chocolate, Size(100, 100))

        result = redactor.apply(PageAreaRedaction("[a-z]+", text_options, image_options))
        if result.status != RedactionStatus.FAILED:
            result_path = redactor.save()
            print("Output saved to " + result_path)


if __name__ == "__main__":
    use_page_area_redaction()
```
{{< /tab >}}
{{< tab "multipage_sample.pdf" >}}
{{< tab-text >}}
`multipage_sample.pdf` is the sample file used in this example. Click [here](/redaction/python-net/_sample_files/developer-guide/advanced-usage/using-redaction-filters/use-page-area-redaction/multipage_sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multipage_sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 3.5 MB)
```
[Download full output](/redaction/python-net/_output_files/developer-guide/advanced-usage/using-redaction-filters/use-page-area-redaction/use_page_area_redaction/multipage_sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}

A page area is measured in points from the page's top-left corner. Read a page's size from `redactor.get_document_info().pages`, as the [PDF redaction filters]({{< ref "redaction/python-net/developer-guide/advanced-usage/using-redaction-filters/use-pdf-redaction-filters.md" >}}) example does.
