---
id: how-to-run-examples
url: redaction/java/how-to-run-examples
title: How to Run Examples
weight: 6
description: Learn how to run all Java examples for GroupDocs.Redaction. Step-by-step guide to clone the repository, install dependencies, and execute all examples using Maven.
keywords: run examples, Java examples, Maven, run all examples, code examples, tutorial
productName: GroupDocs.Redaction for Java
hideChildren: False
---

## Prerequisites

Before running the examples, ensure you have:

- **Java JDK 8 or later** (JDK 17 LTS recommended) - See [System Requirements]({{< ref "redaction/java/getting-started/system-requirements.md" >}})
- **Maven 3.6 or later** - For building and running examples
- **Git** - To clone the repository (optional)

## Getting the Examples

### Option 1: Clone from GitHub

Clone the repository to your local machine:

```bash
git clone https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java.git
cd GroupDocs.Redaction-for-Java
```

### Option 2: Download ZIP

Download the repository as a ZIP file from [GitHub](https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java) and extract it.

## Installation

Navigate to the `Examples` directory and install dependencies:

```bash
cd Examples
mvn clean install
```

This command will:
- Download the GroupDocs.Redaction library and all required dependencies
- Compile all example classes
- Prepare the project for execution

## Running All Examples

Execute all examples using Maven:

```bash
cd Examples
mvn compile exec:java
```

This will run all examples sequentially. Output files are saved to `target/Output/<example-name>/`.

## Output Location

All example outputs are saved to:

```
Examples/target/Output/<example-name>/
```

For example:
- `HelloWorld` example → `target/Output/HelloWorld/`
- `ApplyRedaction` example → `target/Output/ApplyRedaction/`

## Troubleshooting

### Maven Build Errors

If dependencies fail to download:

```bash
# Clean and rebuild
mvn clean install -U
```

### Java Version Issues

Ensure you're using Java 8 or later:

```bash
java -version
javac -version
```

Set `JAVA_HOME` environment variable if needed.

### Missing Sample Files

Ensure all sample files are present in `Examples/Resources/SampleFiles/`. If files are missing, examples may fail.

### License Warnings

Examples run in trial mode by default. To remove license warnings:

1. Get a temporary license from [GroupDocs](https://purchase.groupdocs.com/temp-license/100510)
2. Update `Constants.java` with your license path
3. Run `SetLicenseFromFile` example

## Repository

View the complete source code and examples on GitHub:

**https://github.com/groupdocs-redaction/GroupDocs.Redaction-for-Java**