---
id: licensing-and-subscription
url: redaction/python-net/licensing-and-subscription
title: Licensing and evaluation
weight: 5
keywords: free, free trial, subscription, evaluation, groupdocs redaction python
description: "GroupDocs.Redaction for Python via .NET offers flexible licensing options, including a Free Trial and a 30-day Temporary License for evaluation purposes."
productName: GroupDocs.Redaction for Python via .NET
hideChildren: False
toc: True
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

Use the [set_license](https://reference.groupdocs.com/redaction/python-net/groupdocs.redaction/license/set_license/) method to license the component. Calling it more than once is harmless — it simply wastes a little processor time.

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
        License().set_license(license_path)
        print("License set successfully.")
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

- Only **one document** can be opened per process (a subsequent open raises a `TrialLimitationsException`).
- Only **one redaction** can be applied to the document.
- Any redaction is limited to **four replacements/deletions**, even if there are more matches.
- Trial badges are placed at the top of each page of the output document.

### Temporary License

To experience the complete features of GroupDocs.Redaction without the limitations of the Free Trial, you can request a 30-day ["Temporary License"](https://purchase.groupdocs.com/temporary-license).
