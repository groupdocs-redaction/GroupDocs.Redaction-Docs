---
id: installation
url: redaction/java/installation
title: Installation
weight: 4
description: Learn how to install GroupDocs.Redaction for Java in your project. Step-by-step guide for adding the library dependency using Maven, Gradle, Kotlin, Ivy, or Sbt build tools. Includes repository configuration and dependency declaration.
keywords: installation, Maven, Gradle, dependency, repository, install GroupDocs Redaction, Java library, build tools, pom.xml, build.gradle
productName: GroupDocs.Redaction for Java
hideChildren: False
---

GroupDocs.Redaction for Java is distributed via the [GroupDocs Repository](https://releases.groupdocs.com/java/repo/). You can easily add it to your project using any Java build tool (Maven, Gradle, Kotlin, Ivy, or Sbt) with simple configuration.

> **Note:** The current version shown below is **25.12**. Always check the [releases page](https://releases.groupdocs.com/java/repo/com/groupdocs/groupdocs-redaction/) for the latest version.

### Specify GroupDocs Repository Configuration

First, you need to specify repository configuration/location in your project as follows:

{{< tabs "example1">}}
{{< tab "Maven" >}}
```xml
<repositories>
	<repository>
		<id>GroupDocs Artifact Repository</id>
        	<name>GroupDocs Artifact Repository</name>
        	<url>https://releases.groupdocs.com/java/repo/</url>
	</repository>
</repositories>
```
{{< /tab >}}
{{< tab "Gradle" >}}
```xml
repositories {
    maven {
        url "https://releases.groupdocs.com/java/repo/"
    }
}
```
{{< /tab >}}
{{< tab "Kotlin" >}}
```xml
repositories {
    maven(url = "https://releases.groupdocs.com/java/repo/")
}
```
{{< /tab >}}
{{< tab "Ivy" >}}
```xml
<ivysettings>
    <settings defaultResolver="chain"/>
    <resolvers>
        <chain name="chain">
            <ibiblio name="GroupDocs Repository" m2compatible="true" root="https://releases.groupdocs.com/java/repo/"/>
        </chain>
    </resolvers>
</ivysettings>
```
{{< /tab >}}
{{< tab "Sbt" >}}
```xml
resolvers += Resolver.url("GroupDocs Repository", url("https://releases.groupdocs.com/java/repo/"))
```
{{< /tab >}}
{{< /tabs >}}

### Add GroupDocs.Redaction as a dependency

Then define GroupDocs.Redaction for Java API dependency in your project as follows:

{{< tabs "example2">}}
{{< tab "Maven" >}}
```xml
<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-redaction</artifactId>
        <version>25.12</version>
    </dependency>
</dependencies>
```
{{< /tab >}}
{{< tab "Gradle" >}}
```xml
dependencies {
    implementation 'com.groupdocs:groupdocs-redaction:25.12'
}
```
{{< /tab >}}
{{< tab "Kotlin" >}}
```xml
dependencies {
    implementation("com.groupdocs:groupdocs-redaction:25.12")
}
```
{{< /tab >}}
{{< tab "Ivy" >}}
```xml
<dependency org="com.groupdocs" name="groupdocs-redaction" rev="25.12">
   <artifact name="groupdocs-redaction" ext="jar"/>
</dependency>
```
{{< /tab >}}
{{< tab "Sbt" >}}
```xml
libraryDependencies += "com.groupdocs" % "groupdocs-redaction" % "25.12"
```
{{< /tab >}}
{{< /tabs >}}

## Verification

After performing the above steps, GroupDocs.Redaction for Java dependency will be added to your project. Verify the installation by:

1. **Building your project:**
   ```bash
   mvn clean install
   # or
   ./gradlew build
   ```

2. **Checking dependencies:**
   ```bash
   mvn dependency:tree | grep groupdocs-redaction
   # or
   ./gradlew dependencies | grep groupdocs-redaction
   ```

## Next Steps

- Review [System Requirements]({{< ref "redaction/java/getting-started/system-requirements.md" >}}) to ensure compatibility
- Check [Supported Document Formats]({{< ref "redaction/java/getting-started/supported-document-formats.md" >}})
- Learn how to [Run Examples]({{< ref "redaction/java/getting-started/how-to-run-examples.md" >}})
