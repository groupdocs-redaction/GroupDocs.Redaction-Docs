---
id: use-advanced-logging
url: redaction/java/use-advanced-logging
title: Use advanced logging
weight: 4
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---

You can implement *ILogger* interface from com.groupdocs.redaction.options package. This interface requires to implement three methods:



```java
import com.groupdocs.redaction.options.ILogger;
import java.util.ArrayList;
/**
 * <p>
 * This is an example of ILogger implementation, tracking count of error messages.
 * </p>
 */
public class CustomLogger implements ILogger
{
    private ArrayList<String> _errors;
    private ArrayList<String> _traces;
    private ArrayList<String> _warnings;
    public boolean hasErrors() 
    { 
        return _errors.size() > 0; 
    }
    public CustomLogger()
    {
        _errors = new ArrayList<String>();
        _traces = new ArrayList<String>();
        _warnings = new ArrayList<String>();
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
```

Once implemented, you can use it to track error log records:



```java
CustomLogger logger = new CustomLogger();
final Redactor redactor = new Redactor(Constants.SAMPLE_DOCX, new LoadOptions(), new RedactorSettings(logger));
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
