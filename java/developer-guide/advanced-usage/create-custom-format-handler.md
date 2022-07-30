---
id: create-custom-format-handler
url: redaction/java/create-custom-format-handler
title: Create custom format handler
weight: 6
description: "This article shows how to implement one or several interfaces for the document's features and required redaction."
keywords: redaction
productName: GroupDocs.Redaction for Java
hideChildren: False
---
If format is not supported, you will need to implement a handler for it by inheriting from *DocumentFormatInstance* class. Depending on the document's features and required redactions, you will also need to implement one or several interfaces, allowing GroupDocs.Redaction to work with this document format.

| Interface | Description |
| --- | --- |
| *ITextualFormatInstance* | Required for document text redactions to work, replaces occurrences of given regular expression with text or a color block |
| *IMetadataAccess* | Required for metadata redactions, reads metadata and changes specific metadata item |
| *IAnnotatedDocument* | Required for annotation redactions, changes or deletes annotations, matching given regular expression |
| *IRasterizableDocument* | Required to rasterize (save document as a PDF with page images) |
| *IImageFormatInstance* | Required for raster image format redactions, based on area top-left corner coordinates and area size |
| *IPreviewable* | Required to provide document general information and preview functionality |

Each of these interfaces is optional, i.e. you don't have to implement all of them, e.g. *IImageFormatInstance* - if you don't need its functionality or *IMetadataAccess*, if your format does not support metadata.

Below, we create a *DocumentFormatInstance* class with custom logic for textual documents processing, supporting only textual redactions:



```java
import com.groupdocs.redaction.options.RedactorSettings;

public class CustomTextualDocument extends DocumentFormatInstance implements ITextualFormatInstance
{
    private RedactorSettings _settings;
    private final java.util.List<String> _fileContent;
 
    public CustomTextualDocument()
    {
        _fileContent = new java.util.ArrayList<>();
    }
 
    @Override
    public void initialize(DocumentFormatConfiguration config, RedactorSettings settings)
    {
        _settings = settings;
    }
 
    @Override
    public void load(java.io.InputStream input) throws java.lang.Exception
    {
        _fileContent.clear();
        java.io.BufferedReader reader = new java.io.BufferedReader(
                new java.io.InputStreamReader(input)
        );
        String line = reader.readLine();
        while (line != null)
        {
            _fileContent.add(line);
            line = reader.readLine();
        }            
        reader.close();
    }
 
    @Override
    public void save(java.io.OutputStream output) throws java.lang.Exception
    {
        java.io.BufferedWriter writer = new java.io.BufferedWriter(new java.io.OutputStreamWriter(output));
        for (String line : _fileContent)
        {
            writer.write(line);
        }
        writer.close();
    }
 
    @Override
    public RedactionResult replaceText(java.util.regex.Pattern regex, ReplacementOptions options)
    {
        try
        {
            if (options.getActionType() != ReplacementType.ReplaceString)
            {
                return RedactionResult.failed("This format allows only ReplaceString redactions!");
            }
            for (int i = 0; i < _fileContent.size(); i++)
            {
                _fileContent.set(i, regex.matcher(_fileContent.get(i)).replaceAll(options.getReplacement()));
            }
            return RedactionResult.successful();
        }
        catch (java.lang.Exception ex)
        {
            return RedactionResult.failed(ex.getMessage());
        }
    }
}
```

In order to use this class, we will need to add it to pre-configured formats, e.g. as a handler for dump files ("\*.dump"):



```java
DocumentFormatConfiguration format = new DocumentFormatConfiguration();
format.setExtensionFilter(".dump");
format.setDocumentType(typeof(CustomTextualDocument));

RedactorConfiguration config = DocumentFormatInstance.getDefaultConfiguration();
config.getAvailableFormats().add(format);
```

### Security and password protection

If your format supports security options like password protection, you'll have to pass true or false to *SetAccessGranted* method of *DocumentFormatInstance* class in your override of *Load* method and throw IncorrectPasswordException or PasswordRequiredException, if applicable. For instance:



```java
@Override
public void load(java.io.InputStream input) throws java.lang.Exception
{
    try
    {
		// check security and load document 

        setAccessGranted(true);
    }
    catch (SomeSecurityException ex)
    {
        setAccessGranted(false);
		// Password, provided with LoadOptions
        if (string.IsNullOrEmpty(Password))
            throw new Exceptions.PasswordRequiredException();
        else
            throw new Exceptions.IncorrectPasswordException();
    }
}

```
