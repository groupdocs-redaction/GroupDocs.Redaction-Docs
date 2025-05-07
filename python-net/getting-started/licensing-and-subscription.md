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

After purchasing GroupDocs.Redaction for Python via .NET, you will receive a license file that needs to be applied to unlock the full functionality of the API. 

License Application Requirements:
- The license should be set only once within the application domain
- It must be configured before using any GroupDocs.Redaction classes
    
### License Applying Options

Licenses can be applied from different locations:

*   Explicit path
*   The folder containing the _GroupDocs.Redaction.dll_ file
*   The folder containing the assembly that called _GroupDocs.Redaction.dll_
*   The folder containing the entry assembly (your _.exe_)
*   As a Metered License that allows you to pay for your usage. For details, see the [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered/).

When you reference _GroupDocs.Redaction.dll_ in the application, the library is copied to your output directory (unless **Copy Local** in the properties for that entry is set to false). The easiest way to set a license is often to place the license file in the same folder as _GroupDocs.Redaction.dll_ and specify just the filename without the path.

Use the [setLicense](https://reference.groupdocs.com/redaction/net/groupdocs.redaction/license/setlicense/) method to license a component.

Calling `setLicense` multiple times is not harmful, it simply wastes processor time.

Calling [setMeteredKey](https://reference.groupdocs.com/redaction/net/groupdocs.redaction/metered/setmeteredkey/) multiple times is not harmful either but wastes processor time and can accumulate consumption improperly.

#### Apply the License

After obtaining the license, set it. This section explains how to do this. When developing your application, call the `setLicense` method in your startup code before using the GroupDocs.Redaction classes.

##### Set a License from a File

The following code snippet shows how to set a license from file:

{{< tabs "example1">}}
{{< tab "Python" >}}

```python
def run():
    if os.path.exists("path to .lic file"):    
        license = gr.License()
        license.set_license("path to .lic file")
        print("License set successfully.")
    else:
       print("\n")
```

{{< /tab >}}
{{< /tabs >}}

##### Set a License from a Stream

The following code snippet shows how to set a license from a stream:

{{< tabs "example2">}}
{{< tab "Python" >}}

```python
if os.path.exists("path to .lic file"):
        with open("path to .lic file", "rb") as stream:
            gr.License().set_license(stream)

        print("License set successfully.")
    else:
        print("\n")
```

{{< /tab >}}
{{< /tabs >}}

### Changing the License File Name

You are not required to keep the license file name as GroupDocs.Redaction.lic. You can rename it to any preferred name and use that name when applying the license in your application.

### "Cannot find license filename" Exception

When you download the license from the GroupDocs website, it is saved with the name GroupDocs.Redaction.lic. However, some web browsers may automatically append .xml, resulting in the file name being GroupDocs.Redaction.lic.xml.

If your Windows settings are configured to hide file extensions (which is the default), the file may still appear as GroupDocs.Redaction.lic in File Explorer, even though the actual name is GroupDocs.Redaction.lic.xml. This discrepancy can cause the `setLicense` method to throw an exception.

To fix this issue, manually rename the file to remove the .xml extension. Optionally, disable the "Hide extensions for known file types" option in Windows to prevent this issue.

## How to Evaluate GroupDocs.Redaction

You can evaluate GroupDocs.Redaction for Python via .NET without purchasing a license by using one of the following options:

### Free Trial

The evaluation version is identical to the purchased one; it becomes licensed once you set the license. You can set the license using methods described in the following sections of this article.

The Free Trial version gives you access to the API's features, but with some limitations:

- Only 1 document can be opened in one process.
- Only 1 redaction can be applied to the document.
- Any redaction is limited to 4 replacements/deletions, even if there are more matches.
- Trial badges are placed in the document on the top of each page.

### Temporary License

To experience the complete features of GroupDocs.Redaction without the limitations of the Free Trial, you can request a 30-day ["Temporary License"](https://purchase.groupdocs.com/temporary-license).