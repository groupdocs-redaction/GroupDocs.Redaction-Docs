---
id: evaluation-limitations-and-licensing
url: redaction/java/evaluation-limitations-and-licensing
title: Evaluation Limitations and Licensing
weight: 5
description: free trial api version for redaction is available to evaluate the API which will be similar as licensed but with few limitations.
keywords: redaction,license,free trial,api  
productName: GroupDocs.Redaction for Java
hideChildren: False
---
{{< alert style="info" >}}You can use GroupDocs.Redaction without the license. The usage and functionalities are pretty much same as the licensed one but you will face few limitations while using the non-licensed API.{{< /alert >}}

## Evaluation Limitations

You can easily download GroupDocs.Redaction for evaluation. The evaluation download is the same as the purchased download. The evaluation version simply becomes licensed when you add a few lines of code to apply the license. You will face following limitations while using the API without the license:  

*   Only 1 document can be opened in one process.
*   Only 1 redaction can be applied to the document.
*   Any redaction is limited to 4 replacements/deletions, even if there are more matches.
*   Trial badges are placed in the document on the top of each page.

## Licensing

The license file contains details such as the product name, number of developers it is licensed to, subscription expiry date and so on. It contains the digital signature, so don't modify the file. Even inadvertent addition of an extra line break into the file will invalidate it. You need to set a license before utilizing GroupDocs.Redaction API if you want to avoid its evaluation limitations. 

  
The license can be loaded from a file or stream object.

#### Applying License from File

The code below will explain how to apply product license.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
// Setup the license.
License lic = new License();
lic.setLicense(licensePath);
```

#### Applying License from Stream

The following example shows how to load a license from a stream.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
final FileInputStream stream = new FileInputStream(licensePath);
try 
{
    License license = new License();
    license.setLicense(stream);
}
finally { stream.close(); }
```
{{< alert style="info" >}}
Calling License.SetLicense multiple times is not harmful but simply wastes processor time. If you are developing a Windows Forms or console application, call License.SetLicense in your startup code, before using GroupDocs.Redaction classes.  
{{< /alert >}}
#### Applying Metered License
{{< alert style="info" >}}
You can also set [Metered](https://apireference.groupdocs.com/net/viewer/groupdocs.viewer/metered) license as an alternative to license file. It is a new licensing mechanism that will be used along with existing licensing method. It is useful for the customers who want to be billed based on the usage of the API features. For more details, please refer to [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered) section.
{{< /alert >}}
Here are the simple steps to use the `Metered` class.
1.  Create an instance of `Metered` class.
2.  Pass public & private keys to `setMeteredKey` method.
3.  Do processing (perform task).
4.  call method `getConsumptionQuantity` of the `Metered` class.
5.  It will return the amount/quantity of API requests that you have consumed so far.
6.  call method `getConsumptionCredit` of the `Metered` class.
7.  It will return the credit that you have consumed so far.

Following is the sample code demonstrating how to use `Metered` class.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java
String privateKey = "[Your Dynabic.Metered private key]";
String publicKey = "[Your Dynabic.Metered public key]";
Metered metered = new Metered();
metered.setMeteredKey(publicKey, privateKey);

final Redactor redactor = new Redactor("D:\Sample.docx");
try 
{
    // Do some redaction
    RedactorChangeLog result = redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions(java.awt.Color.RED)));
    // and get consumption quantity
    double consumptionQuantitiy = Metered.getConsumptionQuantity();
    // get consumption credit 
    double consumptionCredit = Metered.getConsumptionCredit();
}
finally { redactor.close(); }
```
