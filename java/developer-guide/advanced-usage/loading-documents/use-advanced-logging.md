---
id: use-advanced-logging
url: redaction/java/use-advanced-logging
title: Use advanced logging
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
toc: True
---

You can implement *ILogger* interface from com.groupdocs.redaction.options package. This interface requires to implement three methods. Once implemented, you can use it to track error log records:

{{< tabs "code-example-use-advanced-logging" >}}
{{< tab "use_advanced_logging.java" >}}
```java
public class CustomLogger implements ILogger
{
    private ArrayList<String> _errors = new ArrayList<String>();
    private ArrayList<String> _traces = new ArrayList<String>();
    private ArrayList<String> _warnings = new ArrayList<String>();

    public boolean hasErrors()
    {
        return _errors.size() > 0;
    }

    public void error(String message)
    {
        _errors.add(message);
    }

    public void trace(String message)
    {
        _traces.add(message);
    }

    public void warning(String message)
    {
        _warnings.add(message);
    }
}

CustomLogger logger = new CustomLogger();
final Redactor redactor = new Redactor("sample.docx", new LoadOptions(), new RedactorSettings(logger));
try
{
    // Here we can use document instance to perform redactions
    redactor.apply(new DeleteAnnotationRedaction());
    if (!logger.hasErrors())
    {
        redactor.save();
    }
}
finally { redactor.close(); }
```
{{< /tab >}}
{{< tab "sample.docx" >}}
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/redaction/java/_sample_files/developer-guide/advanced-usage/loading-documents/use-advanced-logging/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample_Redacted.pdf" >}}  
```text
Binary file (PDF, 1.2 MB)
```
[Download full output](/redaction/java/_output_files/developer-guide/advanced-usage/loading-documents/use-advanced-logging/CodeExampleUseAdvancedLogging/sample_Redacted.pdf)
{{< /tab >}}
{{< /tabs >}}
