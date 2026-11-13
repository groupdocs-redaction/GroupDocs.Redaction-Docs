---
id: licensing-and-evaluation
url: redaction/python-net/licensing-and-evaluation
title: Licensing and evaluation
weight: 5
keywords: free, free trial, subscription, evaluation, evaluation limitations, license, metered license, set_license, is_licensed, set_metered_key, GROUPDOCS_LIC_PATH, LicenseError, groupdocs redaction python
description: "GroupDocs.Redaction for Python via .NET offers flexible licensing options, including a Free Trial and a 30-day Temporary License for evaluation purposes."
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
aliases:
    - /redaction/python-net/licensing-and-subscription/
---

To explore the system effectively, you may want immediate access to the API. GroupDocs.Redaction simplifies this by offering various purchase plans, along with a Free Trial and a 30-day Temporary License for evaluation.

{{< alert style="info" >}}

To learn more about licensing options, purchasing, and evaluation policies, refer to the [Purchase Policies and FAQ](https://purchase.groupdocs.com/policies) section.

{{< /alert >}}

## Purchased License

After purchasing GroupDocs.Redaction for Python via .NET, you will receive a license file that unlocks the full functionality of the API. A few rules apply:

- Apply the license **only once** per process, in your start-up code.
- Apply it **before** constructing any `Redactor` or other GroupDocs.Redaction object.
- A license can be applied from a file path, from a binary stream (handy when the license is an embedded resource), or as a [Metered License](https://purchase.groupdocs.com/faqs/licensing/metered/) that bills by usage.

Use the [set_license](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/license/set_license/) method to license the component, and its `is_licensed` property to check the result. Calling it more than once is harmless — it simply wastes a little processor time.

### Set a license from a file

The example below applies a license from a file path. It reads the path from the `GROUPDOCS_LIC_PATH` environment variable and falls back to a local `GroupDocs.Redaction.lic` file:

{{< tabs "code-example-set-license-from-file" >}}
{{< tab "set_license_from_file.py" >}}
```python
import os
from groupdocs.redaction import License

def set_license_from_file():
    # Resolve the license path from the environment, with a local fallback
    license_path = os.environ.get("GROUPDOCS_LIC_PATH", "./GroupDocs.Redaction.lic")

    # Apply the license before using any redaction features
    if os.path.exists(license_path):
        license = License()
        license.set_license(license_path)
        print("License set successfully:", license.is_licensed)
    else:
        print("License file not found. Running in evaluation mode.")

if __name__ == "__main__":
    set_license_from_file()
```
{{< /tab >}}
{{< /tabs >}}

### Set a license from a stream

You can also apply a license from any readable binary stream — useful when the license ships as an embedded resource:

{{< tabs "code-example-set-license-from-stream" >}}
{{< tab "set_license_from_stream.py" >}}
```python
import os
from groupdocs.redaction import License

def set_license_from_stream():
    # Resolve the license path from the environment, with a local fallback
    license_path = os.environ.get("GROUPDOCS_LIC_PATH", "./GroupDocs.Redaction.lic")

    # Apply the license from an open binary stream
    if os.path.exists(license_path):
        with open(license_path, "rb") as stream:
            License().set_license(stream)
        print("License set successfully.")
    else:
        print("License file not found. Running in evaluation mode.")

if __name__ == "__main__":
    set_license_from_stream()
```
{{< /tab >}}
{{< /tabs >}}

### Set a license from an environment variable

Set `GROUPDOCS_LIC_PATH` to the license file's path, or to a URL that serves it, and the license is applied at the first call into the engine, with no licensing code:

{{< tabs "env-license">}}
{{< tab "Windows" >}}
```ps
$env:GROUPDOCS_LIC_PATH = "C:\licenses\GroupDocs.Redaction.lic"
```
{{< /tab >}}
{{< tab "Linux / macOS" >}}
```bash
export GROUPDOCS_LIC_PATH="/opt/licenses/GroupDocs.Redaction.lic"
```
{{< /tab >}}
{{< /tabs >}}

A license that cannot be applied (a missing file, an expired subscription, a license for another product) raises `LicenseError` from the first call into the engine on, rather than letting the process run in evaluation mode unnoticed. The message names the variable and the engine's reason. Set `GROUPDOCS_LIC_STRICT=0` to get a `LicenseWarning` and evaluation mode instead. When `GROUPDOCS_LIC_PATH` is not set, `ASPOSE_LIC_PATH` is read instead.

A file that is not a license at all, passed to `set_license()`, raises `GroupDocsRedactionException` ("Data at the root level is invalid"), and the process is unlicensed afterwards, even if a license had been applied before.

### Set a metered license

A Metered License lets you pay for what you use. Set the public and private keys with [set_metered_key](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/metered/set_metered_key/) before using the API, then query consumption at any time:

{{< tabs "code-example-set-metered-license" >}}
{{< tab "set_metered_license.py" >}}
```python
from groupdocs.redaction import Metered

def set_metered_license():
    # Replace these placeholders with your real metered public/private keys
    public_key = "*****"
    private_key = "*****"

    # Skip the call until real keys are supplied (placeholder keys are rejected)
    if "*" in public_key or "*" in private_key:
        print("Provide real metered keys to enable metered licensing.")
        return

    # Apply the metered keys before using any redaction features
    Metered().set_metered_key(public_key, private_key)

    # Query the current metered consumption
    quantity = Metered().get_consumption_quantity()
    credit = Metered().get_consumption_credit()
    print(f"Consumption quantity: {quantity}, credit: {credit}")

if __name__ == "__main__":
    set_metered_license()
```
{{< /tab >}}
{{< /tabs >}}

### Changing the license file name

You are not required to keep the license file name as `GroupDocs.Redaction.lic`. You can rename it to any preferred name and use that name when applying the license in your application.

### "Cannot find license filename" exception

When you download the license from the GroupDocs website it is saved as `GroupDocs.Redaction.lic`. However, some web browsers may automatically append `.xml`, resulting in `GroupDocs.Redaction.lic.xml`.

If your Windows settings are configured to hide file extensions (the default), the file may still appear as `GroupDocs.Redaction.lic` in File Explorer even though the actual name is `GroupDocs.Redaction.lic.xml`. This discrepancy can cause `set_license` to throw an exception. To fix it, manually rename the file to remove the `.xml` extension, or disable "Hide extensions for known file types" in Windows.

## How to evaluate GroupDocs.Redaction

You can evaluate GroupDocs.Redaction for Python via .NET without purchasing a license by using one of the following options.

### Free Trial

The evaluation version is identical to the purchased one; it becomes fully licensed once you set a license. Without a license the Free Trial gives you access to the API's features, but with some limitations:

- Up to **25 documents** can be opened per process. The next open raises a `TrialLimitationsException` ("Trial mode allows opening up to 25 documents per process").
- Saved documents carry a red evaluation notice ("Created with evaluation version of GroupDocs.Redaction") at the top of each page.
- Long documents are cut short:
  - a rasterized PDF keeps its first 4 pages;
  - a long Word document saved in its own format loses part of its text: a 10-page document kept 152 of its 276 paragraphs;
  - on a PDF of more than 4 pages, `get_document_info()` raises "At most 4 elements (for any collection) can be viewed in evaluation mode", and page and metadata redactions report `FAILED` or `SKIPPED`.

The number of redactions and replacements is not limited. Releases up to 26.6 also allowed only one document per process, one redaction per document and four replacements per redaction. Judge the completeness of the output with a license applied.

### Temporary License

To experience the complete features of GroupDocs.Redaction without the limitations of the Free Trial, you can request a 30-day ["Temporary License"](https://purchase.groupdocs.com/temporary-license).
