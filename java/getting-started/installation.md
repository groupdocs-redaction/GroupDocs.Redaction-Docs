---
id: installation
url: redaction/java/installation
title: Installation
weight: 4
description: ""
keywords:
productName: GroupDocs.Redaction for Java
hideChildren: False
---
GroupDocs hosts all Java APIs on [GroupDocs Repository](https://releases.groupdocs.com/java/repo/). You can easily use GroupDocs.Redaction for Java API directly in your Maven projects with simple configurations.

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
        url "https://repository.groupdocs.com/repo/"
    }
}
```
{{< /tab >}}
{{< tab "Kotlin" >}}
```xml
repositories {
    maven(url = "https://repository.groupdocs.com/repo/")
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
        <version>24.9</version>
    </dependency>
</dependencies>
```
{{< /tab >}}
{{< tab "Gradle" >}}
```xml
dependencies {
    implementation 'com.groupdocs:groupdocs-redaction:24.9'
}
```
{{< /tab >}}
{{< tab "Kotlin" >}}
```xml
dependencies {
    implementation("com.groupdocs:groupdocs-redaction:24.9")
}
```
{{< /tab >}}
{{< tab "Ivy" >}}
```xml
<dependency org="com.groupdocs" name="groupdocs-redaction" rev="24.9">
   <artifact name="groupdocs-redaction" ext="jar"/>
</dependency>
```
{{< /tab >}}
{{< tab "Sbt" >}}
```xml
libraryDependencies += "com.groupdocs" % "groupdocs-redaction" % "24.9"
```
{{< /tab >}}
{{< /tabs >}}

After performing above-mentioned steps, GroupDocs.Redaction for Java dependency will finally be added to your Maven project.
