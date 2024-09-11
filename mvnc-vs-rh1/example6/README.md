# Example source-level difference between Maven Central and RedHat Earliest

## Overview

This folder shows nonequivalent source code for 2 copies of the class `com.fasterxml.jackson.core.json.PackageVersion` from the Maven project `com.fasterxml.jackson-core.jackson-core:2.17.2`, one taken from Maven Central (mvnc) and the other from RedHat Earliest (rh1).
Each `.diff` file is produced using a command of the form `diff gaoss/X mvnc/X > X.diff`.
The two subdirectories contain the original source jars from each provider and relevant files extracted from them, for convenience.

- File path within both source jars: `com/fasterxml/jackson/core/json/PackageVersion.java`
- Maven Central source jar URL: repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.17.2/jackson-core-2.17.2-sources.jar
- RedHat source jar URL: https://maven.repository.redhat.com/ga/com/fasterxml/jackson/core/jackson-core/2.17.2/jackson-core-2.17.2-sources.jar
- `*.md5` files are at the same URLs with `.md5` appended
- `MANIFEST.MF`, `pom.xml` and `pom.properties` files are extracted from the respective source jars

## Summary of differences

The only Java source code difference between the jars is a version string in `PackageVersion.java`, which is generated automatically by `maven-replacer-plugin`.

Outside of source files, pom.properties` differs between source jars in the same way. `pom.xml` contains more substantial changes, including comments mentioning manual changes on 03-May-2022 and 16-Nov-2022.
