example of different metadata

# Example metadata difference between Maven Central and RedHat Earliest

## Overview

This folder comparies 2 binary jars for the Maven project `commons-io:commons-io:2.15.1`, one taken from Maven Central (mvnc) and the other from RedHat Earliest (rh1).
The two subdirectories contain the original jars from each provider and relevant files extracted from them, for convenience.
`jar.diff` is produced by running `diff -r` on the extracted contents of the 2 binary jars; each other `.diff` file is produced using a command of the form `diff gaoss/X mvnc/X > X.diff`.

- Maven Central binary jar URL: https://repo1.maven.org/maven2/commons-io/commons-io/2.15.1/commons-io-2.15.1.jar
- Maven Central source jar URL: https://repo1.maven.org/maven2/commons-io/commons-io/2.15.1/commons-io-2.15.1-sources.jar
- RedHat binary jar path: https://maven.repository.redhat.com/ga/commons-io/commons-io/2.15.1.redhat-00001/commons-io-2.15.1.redhat-00001.jar
- RedHat source jar path: https://maven.repository.redhat.com/ga/commons-io/commons-io/2.15.1.redhat-00001/commons-io-2.15.1.redhat-00001-sources.jar
- `*.md5` files are at the same paths with `.md5` appended
- `MANIFEST.MF`, `pom.properties` and `pom.xml` are extracted from the respective binary jars

## Summary of differences

The jars differ in 3 metadata files: `MANIFEST.MF` (notably the `Build-Jdk-Spec` fields are different -- `21` for mvnc vs. `1.8` for mvnc), `pom.properties` and `pom.xml`.
Thus the hashes of the jars are different: [84351f7991a0e6722f00e96a4ccc376f for mvnc](https://repo1.maven.org/maven2/commons-io/commons-io/2.15.1/commons-io-2.15.1.jar.md5), [b8e4f1e224679239c6b7c32e74c419d0 for rh1](https://maven.repository.redhat.com/ga/commons-io/commons-io/2.15.1.redhat-00001/commons-io-2.15.1.redhat-00001.jar.md5).

The 323 `Binary files ... differ` lines in `jar.diff` indicate that 323 of the 365 class files also differ betwen the two binary jars.
There is also a file, `versions`, which is present in mvnc but missing in rh1.
