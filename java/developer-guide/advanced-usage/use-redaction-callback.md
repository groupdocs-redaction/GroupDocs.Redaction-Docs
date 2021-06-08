---
id: use-redaction-callback
url: redaction/java/use-redaction-callback
title: Use redaction callback
weight: 3
description: ""
keywords: 
productName: GroupDocs.Redaction for Java
hideChildren: False
---
In order to reject specific changes during redaction process or to keep a full log of changes in the document, you need to set Redactor.RedactionCallback property, to a class implementing IRedactionCallback interface. The interface contains only one method, AcceptRedaction, which receives detailed information about proposed redaction and returns Boolean value, accepted or not.

Below, we create a callback class, dumping changes to system console:



```java
public class RedactionDump implements IRedactionCallback
{
    public RedactionDump()
    {
    }
 
    public boolean acceptRedaction(RedactionDescription description)
    {
        System.out.print(description.getRedactionType() + " redaction, " + description.getActionType() + " action, item " + description.getOriginalText() + ". ");
        if (description.getReplacement() != null)
        {
            System.out.print("Text " + description.getReplacement().getOriginalText() + " is replaced with " + description.getReplacement().getReplacement() + ". ");
        }
        System.out.println();
        return true;
    }
}

```

The instance of this class is to be passed to a constructor of the *Redactor* class:



```java
// Assign an instance of callback before using Redactor
final Redactor redactor = new Redactor("\\Sample.docx", new LoadOptions(), new RedactorSettings(new RedactionDump()));
try 
{            
    redactor.apply(new ExactPhraseRedaction("John Doe", new ReplacementOptions("[personal]")));
    redactor.save();
}
finally { redactor.close(); }

```
